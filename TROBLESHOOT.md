# replacement RK1

In slot 4 seeing the following:
```
[root@turingpi ~]$ lsusb
Bus 001 Device 001: ID 1d6b:0002
Bus 002 Device 001: ID 1d6b:0001
[root@turingpi ~]$ tpi advanced msd --node 4
ok
[root@turingpi ~]$ lsusb
Bus 001 Device 001: ID 1d6b:0002
Bus 001 Device 002: ID 05e3:0608
Bus 002 Device 001: ID 1d6b:0001
Bus 001 Device 004: ID 2207:350b
```

which looks good. But initially in slot 3 it did not do the same.
