
# jc.parsers.sysctl
jc - JSON CLI output utility `sysctl -a` command output parser

Note: Since `sysctl` output is not easily parsable only a very simple key/value object will be output. An attempt is made to convert obvious integers and floats. If no conversion is desired, use the `-r` command-line argument or the `raw=True` argument in `parse()`.

Usage (cli):

    $ sysctl -a | jc --sysctl

    or

    $ jc sysctl -a

Usage (module):

    import jc.parsers.sysctl
    result = jc.parsers.sysctl.parse(sysctl_command_output)

Compatibility:

    'linux', 'darwin', 'freebsd'

Examples:

    $ sysctl -a | jc --sysctl -p
    {
      "user.cs_path": "/usr/bin:/bin:/usr/sbin:/sbin",
      "user.bc_base_max": 99,
      "user.bc_dim_max": 2048,
      "user.bc_scale_max": 99,
      "user.bc_string_max": 1000,
      "user.coll_weights_max": 2,
      "user.expr_nest_max": 32
      ...
    }

    $ sysctl -a | jc --sysctl -p -r
    {
      "user.cs_path": "/usr/bin:/bin:/usr/sbin:/sbin",
      "user.bc_base_max": "99",
      "user.bc_dim_max": "2048",
      "user.bc_scale_max": "99",
      "user.bc_string_max": "1000",
      "user.coll_weights_max": "2",
      "user.expr_nest_max": "32",
      ...
    }


## info
```python
info()
```


## process
```python
process(proc_data)
```

Final processing to conform to the schema.

Parameters:

    proc_data:   (dictionary) raw structured data to process

Returns:

    Dictionary. Structured data with the following schema:

    {
      "foo":     string/integer/float,         # best guess based on value
      "bar":     string/integer/float,
      "baz":     string/integer/float
    }


## parse
```python
parse(data, raw=False, quiet=False)
```

Main text parsing function

Parameters:

    data:        (string)  text data to parse
    raw:         (boolean) output preprocessed JSON if True
    quiet:       (boolean) suppress warning messages if True

Returns:

    Dictionary. Raw or processed structured data.

