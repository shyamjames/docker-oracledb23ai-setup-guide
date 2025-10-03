# Oracle Database 23ai Docker Setup 🐳

This guide provides the steps to quickly set up and run an **Oracle Database 23ai** container using Docker.

-----

## 1\. Pull the Docker Image ⬇️

First, pull the latest Oracle Database Free image from the Oracle Container Registry.

```bash
docker pull container-registry.oracle.com/database/free:latest
```

-----

## 2\. Run the Container 🚀

Next, execute the command below to start the database container.

```bash
docker run --name oracle-23ai \
  -v /your/local/directory/path:/scripts \
  -p 1521:1521 -p 5500:5500 \
  -e ORACLE_PWD=password \
  -d container-registry.oracle.com/database/free:latest
```

**Command Breakdown:**

  * `--name oracle-23ai`: Assigns a memorable name to your container.
  * `-v /your/local/directory/path:/scripts`: Mounts a local directory to a directory inside the container. **Change the local path** to your desired directory.
  * `-p 1521:1521 -p 5500:5500`: Maps the container's database and EM Express ports to your local machine.
  * `-e ORACLE_PWD=AStrongPassword`: Sets the password for `SYS`, `SYSTEM`, and `PDBADMIN`. You should change `password` to something more secure. 🔒
  * `-d`: Runs the container in **detached mode** (in the background).

-----

## 3\. Access the Container Shell 🖥️

To enter the running container's command line, use the `docker exec` command.

```bash
docker exec -it oracle-23ai /bin/bash
```

-----

## 4\. Connect with SQL\*Plus 🔗

Once you are inside the container's shell, you can connect to the database using **SQL\*Plus**.

```bash
sqlplus sys as sysdba
```

You will be prompted to enter the password you set in Step 2.

-----

## 5\. Run a Script ⚙️

After connecting to SQL\*Plus, you can run any `.sql` file from your mounted volume using the `@` command. The local directory you have added will be available at `/scripts` inside the container.

To run a file named `your_script.sql`, use the following command at the SQL prompt:

```sql
SQL> @/scripts/your_script.sql
```


## Starting the Container ▶️

If the container is stopped, you can start it again using its name:

```bash
docker start oracle-23ai
```

-----

## Stopping the Container ⏹️

To gracefully stop the running container:

```bash
docker stop oracle-23ai
```
