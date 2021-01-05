#How to install postgresql 10.15 on Ubuntu 20.04

## Step I: Get tar ball of postgresql and untar 

```
wget https://ftp.postgresql.org/pub/source/v10.15/postgresql-10.15.tar.gz
tar -zxvf ./postgresql-10.15.tar.gz
```

## Step II: Do configuration

```
#Change directory to the untar directory
cd ~/postgresql-10.15

#Make a new directory in your home directory.  You can choose whatever directory you have write persimission on

mkdir ~/postgresql #<installation_dir>

#Do the confiration 
./configure --prefix==~/progresql

``` 
> Note: <installation_dir> is the directory which the user has the write permission on.  

Once this configuration completes successfully, you should see it lands like the below:

```
configure: using LDFLAGS=  -Wl,--as-needed
configure: creating ./config.status
config.status: creating GNUmakefile
config.status: creating src/Makefile.global
config.status: creating src/include/pg_config.h
config.status: creating src/include/pg_config_ext.h
config.status: creating src/interfaces/ecpg/include/ecpg_config.h
config.status: linking src/backend/port/tas/dummy.s to src/backend/port/tas.s
config.status: linking src/backend/port/dynloader/linux.c to src/backend/port/dynloader.c
config.status: linking src/backend/port/posix_sema.c to src/backend/port/pg_sema.c
config.status: linking src/backend/port/sysv_shmem.c to src/backend/port/pg_shmem.c
config.status: linking src/backend/port/dynloader/linux.h to src/include/dynloader.h
config.status: linking src/include/port/linux.h to src/include/pg_config_os.h
config.status: linking src/makefiles/Makefile.linux to src/Makefile.port
joyee_zhu@instance-1:~/postgresql-10.15$
```

### Issues you might see during configuration 

You need root's permission to fix the below issues.

#### Issue I:
```
configure: error: in `/home/joyee_zhu/postgresql-10.15':
configure: error: no acceptable C compiler found in $PATH
```
In this case, you need to install c compiler. 

```
sudo apt update
sudo apt install gcc
```
The above commands installed gcc c compiler

#### Issue II:
If you are seeing the following error while you are doing __`configure`__

```
configure: error: readline library not found
```

do the following command
 
```
sudo apt install libreadline-dev
```

#### Issue III:
If you are seeing the following error while you are doing __`configure`__

```
configure: error: zlib library not found
```

Do the following command

```
sudo apt-get install zlib1g-dev
```


## Step III Install

Do the following command to do installation

```
make install 
```

>Note: The installation takes quite a lot of time to complete. Be patient!

Once the install completes successfully, you should see the following lines:

```
make -C config install
make[1]: Entering directory '/home/joyee_zhu/postgresql-10.15/config'
/usr/bin/mkdir -p '/home/joyee_zhu/postgresql/lib/pgxs/config'
/usr/bin/install -c -m 755 ./install-sh '/home/joyee_zhu/postgresql/lib/pgxs/config/install-sh'
/usr/bin/install -c -m 755 ./missing '/home/joyee_zhu/postgresql/lib/pgxs/config/missing'
make[1]: Leaving directory '/home/joyee_zhu/postgresql-10.15/config'
PostgreSQL installation complete.
joyee_zhu@instance-1:~/postgresql-10.15$
```

### Issues you might see during installation 

You need root's permission to fix the below issues.

#### Issue I:

If you are seeing the following error while you are doing __`make install`__

```
Command 'make' not found, but can be installed with:

apt install make        # version 4.2.1-1.2, or
apt install make-guile  # version 4.2.1-1.2

Ask your administrator to install one of them.
```

Do the following command:

```
sudo apt install make
```

## Step IV Check the installation

After the installation, do some basic checkings:

```
cd ~/postgresql
ls ./bin

```

You should see the following files listed out. 

```
joyee_zhu@instance-1:~/postgresql/bin$ ll
total 12324
drwxrwxr-x 2 joyee_zhu joyee_zhu    4096 Jan  5 00:11 ./
drwxrwxr-x 6 joyee_zhu joyee_zhu    4096 Jan  5 00:09 ../
-rwxr-xr-x 1 joyee_zhu joyee_zhu   83864 Jan  5 00:11 clusterdb*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   83656 Jan  5 00:11 createdb*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   84376 Jan  5 00:11 createuser*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   74936 Jan  5 00:11 dropdb*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   74904 Jan  5 00:11 dropuser*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  941584 Jan  5 00:10 ecpg*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  160400 Jan  5 00:10 initdb*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   38408 Jan  5 00:10 pg_archivecleanup*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  139672 Jan  5 00:10 pg_basebackup*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   42064 Jan  5 00:10 pg_config*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   50656 Jan  5 00:10 pg_controldata*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   65720 Jan  5 00:10 pg_ctl*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  431936 Jan  5 00:11 pg_dump*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  118696 Jan  5 00:11 pg_dumpall*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   79016 Jan  5 00:11 pg_isready*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   86224 Jan  5 00:10 pg_receivewal*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   91192 Jan  5 00:10 pg_recvlogical*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   60048 Jan  5 00:11 pg_resetwal*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  198656 Jan  5 00:11 pg_restore*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  102832 Jan  5 00:11 pg_rewind*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   43120 Jan  5 00:11 pg_test_fsync*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   38072 Jan  5 00:11 pg_test_timing*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  154416 Jan  5 00:11 pg_upgrade*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   97808 Jan  5 00:11 pg_waldump*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  148544 Jan  5 00:11 pgbench*
-rwxr-xr-x 1 joyee_zhu joyee_zhu 8232400 Jan  5 00:09 postgres*
lrwxrwxrwx 1 joyee_zhu joyee_zhu       8 Jan  5 00:09 postmaster -> postgres*
-rwxr-xr-x 1 joyee_zhu joyee_zhu  650152 Jan  5 00:11 psql*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   83960 Jan  5 00:11 reindexdb*
-rwxr-xr-x 1 joyee_zhu joyee_zhu   88632 Jan  5 00:11 vacuumdb*
```

Once, you saw above print-out and then you are done with the installation. 

## Step V: Setup environment to get ready to run postgresql

Open your __`~/.bashrc`__ which locates in your home directory.  Add in the following lines. 

```
export POSTGRESQL_HOME=$HOME/postgresql
export PATH=$POSTGRESQL_HOME/bin:$PATH
export LD_LIBRARY_PATH=$POSTGRESQL_HOME/lib:$LD_LIBRARY_PATH
```

After closing the file, please re-source the ~/.bashrc to enable the setup

```
source ~/.bashrc
```

Then do the following command

```
which pg_ctl
```

You should see the following print-out

```
joyee_zhu@instance-1:~/postgresql/lib$ which pg_ctl
/home/joyee_zhu/postgresql/bin/pg_ctl
```

Congratulation, You are Done!