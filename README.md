# gping

gping serves as a wrapper around fping: Given an fping-compatible pattern, it passes said pattern directly to fping, along with flags that tell fping to perform DNS lookups as well as pings. gping then takes the resulting raw output and parses it to determine each IP's "state", based upon its ping response and DNS lookup results:

| Responds to Ping | Has DNS Entry | State   |
| ---------------: | :-----------: | ------- |
| Yes              | Yes           | Awake   |
| No               | Yes           | Asleep  |
| Yes              | No            | Lurking |
| No               | No            | Free    |

By default, it emits its results as terminal output, with the IPs sorted in ascending order, using emoji to indicate each address's state:

| State   | Symbol |
| ------: | :----: |
| awake   | 🙂     |
| asleep  | 💤     |
| lurking | 🌚     |
| free    | 🆓     |

## Flags

By default, it sorts the results by IP address, in ascending order. If passed the "-g" or "--group" flags without arguments, it sorts by state instead. If passed those flags _with_ state arguments, it displays _only_ the hosts in the specified state(s).

    gping 10.141.36.0/24 -g
    gping 10.141.36.0/24 -gfree
    gping 10.141.36.0/24 -gasleep,lurking

If passed the `-j/--json` option, it will emit its results as JSON instead. (**Note**: The format will likely change before 1.0.)

## Warning/Disclaimer

This is a pre-release version. Flags and the exact structure of the JSON output, to name but two, are likely to change before the official 1.0 version.
