# Support Trace

## To build

Usually, you may need to install a dependent package
```
sudo apt-get install libpci-dev
```

Then, in the perftest folder, run
```
./autogen.sh
./configure
make -j
```

## To run

Use the following command at server side
```
./ib_read_bw -d <dev_name> -F -p 10000 --trace_filename <trace_file> -n <trace_length> -x <gid_index>
```

and the following command at client side
```
./ib_read_bw -d <dev_name> -F -p 10000 --trace_filename <trace_file> -n <trace_length> -x <gid_index> <server ip>
```

**Please note** that you need to use `show_gids` to see the device name and the `gid_index` for RoCEv2.
For example, on ds09 ens3f1 and ds10 ens3f1, `show_gids` will tell us that both are using device name `mlx5_1` and `gid_index` 3 for RoCEv2.
Therefore, we have the following commands
```
./ib_read_bw -d mlx5_1 -F -p 10000 --trace_filename ./trace_test.txt -n 79 -x 3
./ib_read_bw -d mlx5_1 -F -p 10000 --trace_filename ./trace_test.txt -n 79 -x 3 10.0.8.5
```
