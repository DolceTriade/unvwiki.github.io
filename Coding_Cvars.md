---
title: Coding Cvars
permalink: /Coding/Cvars/
---

Classes that handle Cvars are defined in .

# Registering Cvars from the sources

Instantiate an object of the correct class with static storage.

### Example

    static Cvar::Cvar<std::string> some_cvar(
        "cvar_name",
        "Cvar description",
        Cvar::NONE,
        "default value"
    );

    Log::Debug("The value of the cvar is %s", some_cvar.Get());
    // Also possible is *some_cvar instead of Get

# Cvar types

## Cvar::Cvar

Allows to define cvars that can hold simple values, while it is a
template it requires a parser and serializer for the type it should
contain.

By default, these types are supported out of the box:

- `Cvar::Cvar`<bool>
- `Cvar::Cvar`<int>
- `Cvar::Cvar`<float>
- `Cvar::Cvar`<std::string>

## Cvar::Callback

This is a curiously recurring wrapper that allows execution of arbitrary
code on cvar changes.

### Example

    static Cvar::Callback<Cvar::Cvar<std::string>> best(
        "best",
        "Who is the best?",
        Cvar::NONE,
        "",
        [](const std::string& name){
            Log::Notice("%s is the best", name);
        }
    );

## Cvar::Callback

This is a curiously recurring wrapper that allows execution of arbitrary
code on cvar changes.

### Example

    static Cvar::Callback<Cvar::Cvar<std::string>> best(
        "best",
        "Who is the best?",
        Cvar::NONE,
        "",
        [](const std::string& name){
            Log::Notice("%s is the best", name);
        }
    );

## Cvar::Modified

This is a curiously recurring wrapper that allows querying whether the
value has changed.

## Cvar::Range

This is a curiously recurring wrapper that limits cvars whose value_type
has a meaningful ordering relation to be within the given range.

### Example

    static Cvar::Range<Cvar::Cvar<int>> percent(
        "percent",
        "%",
        Cvar::NONE,
        100, // default
        0,   // min
        100  // max (inclusive)
    );

## Customizing

Creating customized cvar types with special restrictions is pretty
straightforward.

### Example (Combining existing classes)

    static Cvar::Range<Cvar::Callback<Cvar::Cvar<int>>> bottles_of_beer(
        "bottles_of_beer",
        "Number of bottles of beer on the wall",
        Cvar::NONE,
        99,
        0,
        99,
        [](int n) {
            Log::Notice("%-2d bottles of beer on the wall, %2d bottles of beer.", n, n);
            if ( n > 0 )
            {
                Log::Notice("Take one down, pass it around, %3d bottles of beer on the wall...", n-1);
                bottles_of_beer.Set(n-1);
            }
        }
    );

### Example (Custom class)

    class HexCvar : public Cvar::Cvar<std::string>
    {
    private:
        ::Cvar::OnValueChangedResult Validate(const value_type& value) override
        {
            if ( std::all_of( value.begin(), value.end(), Str::cisxdigit ) )
            {
                return { true, "" };
            }
            return { false, "Must be hex!" };
        }
    };

    static HexCvar cvar_hex(
        "cl_hexString",
        "Must be hex",
        Cvar::NONE,
        ""
    );