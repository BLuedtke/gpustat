`gpustat`
=========

[![license](https://img.shields.io/github/license/wookayin/gpustat.svg?maxAge=86400)](LICENSE)

Just *less* than nvidia-smi?

![Screenshot: gpustat -cp](screenshot.png)

NOTE: This works with NVIDIA Graphics Devices only, no AMD support as of now. Contributions are welcome!

FORKED (by BLuedtke, 2021-06-28).
Added line breaks for each process.


Usage
-----

`$ gpustat`

Options:

* `--color`            : Force colored output (even when stdout is not a tty)
* `--no-color`         : Suppress colored output
* `-u`, `--show-user`  : Display username of the process owner
* `-c`, `--show-cmd`   : Display the process name
* `-f`, `--show-full-cmd`   : Display full command and cpu stats of running process
* `-p`, `--show-pid`   : Display PID of the process
* `-F`, `--show-fan`   : Display GPU fan speed
* `-e`, `--show-codec` : Display encoder and/or decoder utilization
* `-P`, `--show-power` : Display GPU power usage and/or limit (`draw` or `draw,limit`)
* `-a`, `--show-all`   : Display all gpu properties above
* `--watch`, `-i`, `--interval`   : Run in watch mode (equivalent to `watch gpustat`) if given. Denotes interval between updates.
* `--json`             : JSON Output

### Tips

- To periodically watch, try `gpustat --watch` or `gpustat -i`.
    - For older versions, one may use `watch --color -n1.0 gpustat --color`.
- Running `nvidia-smi daemon` (root privilege required) will make the query much **faster** and use less CPU.
- The GPU ID (index) shown by `gpustat` (and `nvidia-smi`) is PCI BUS ID,
  while CUDA differently assigns the fastest GPU with the lowest ID by default.
  Therefore, in order to make CUDA and `gpustat` use **same GPU index**,
  configure the `CUDA_DEVICE_ORDER` environment variable to `PCI_BUS_ID`
  (before setting `CUDA_VISIBLE_DEVICES` for your CUDA program):
  `export CUDA_DEVICE_ORDER=PCI_BUS_ID`.


Quick Installation
------------------

To install the latest version (master branch) via pip:

```
pip install git+https://github.com/BLuedtke/gpustat.git@master
```

Default display
---------------

> [0] GeForce RTX 3070 | 42°C,  4 % | 772 / 7959 MB |    
> \- (memory used by process)

- `[0]`: GPUindex (starts from 0) as PCI_BUS_ID
- `GeForce RTX 3070`: GPU name
- `42°C`: Temperature
- `4 %`: Utilization
- `772 / 7959 MB`: GPU Memory Usage
- `...`: Running processes on GPU (and their memory usage) -> Not final.

Changelog
---------

See [CHANGELOG.md](CHANGELOG.md)


License
-------

[MIT License](LICENSE)
