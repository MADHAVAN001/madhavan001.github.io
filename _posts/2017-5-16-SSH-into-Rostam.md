Today, in my first attempts to ssh into the Rostam Cluster hosted at LSU, was hit with a roadblock but in the process learnt quite a bit about the encryption system and how the public/private keys are used for authentication, though was not relevant to the solution of the problem.

Rostam
----------
Rostam is an all compute node cluster at LSU CCT lab. It has various computing nodes and different machines. Rostam uses SLURM for job scheduling and has been partitioned into many smaller compute cluster. More details about the cluster can be found at [Wiki](https://github.com/STEllAR-GROUP/hpx/wiki/Running-HPX-on-Rostam).

For this project, I would be possibly required to use Bahram/Reno/Tycho, using the following type of commands:

```
srun -p <partition> -N <number-of-nodes> <path-hpx-application> [-n <number-of-processes>] [-c <number-of-cores-per-process>]
```

Setting up OpenSSH to the cluster
-----------------------------------

As such the process is to first generate a public/private key pair using ssh-keygen on Unix based systems or using puttygen for the same in Windows.

Then, the way the system works is to place a public key on the server in ~/.ssh/authorized_keys and then connect to the server with the private key. This ensures that the communication made between the client & server is encrypted and decrypted using relevant keys. This is much more secure than using a password based mechanism for logging in. Key-based authentication mechanism is hard to brute force.

So, the mistake I had commited was to overlook the permissions while creaating and storing the public/private key pairs. They were stored under 'root'. So when I was trying to ssh into the cluster, I was met with the issue of key-file not found. My thought was that the owner of the file shouldn't affect the login process as it was still able to find the file, but just not open it.

So once I changed the owner using sudo chown ubuntu:ubuntu ~/.ssh/key-file it worked perfectly. But the whole process took gruesomely long number of hours and my mentor diehlpk helped me fix this in the end.

A good blog to follow in such a process is [Ubuntu SSH](https://help.ubuntu.com/community/SSH/OpenSSH/Keys)