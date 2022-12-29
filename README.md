# Reproducible experiments for generating pre-processing pipelines for AutoETL

This is the repository for the companion reproducible paper of [1].
To implement the optimization process, we departed from the code provided in [2] (GitHub repository: [https://github.com/aquemy/DPSO_experiments](https://github.com/aquemy/DPSO_experiments)).

[1] J. Giovanelli, B. Bilalli, A. Abelló, "Data pre-processing pipeline generation for AutoETL", Inf. Syst. (2021) 101957. http://dx.doi.org/10.1016/j.is.2021.101957

[2] A. Quemy, "Data Pipeline Selection and Optimization." DOLAP. 2019. http://ceur-ws.org/Vol-2324/Paper19-AQuemy.pdf

# Requirements

In order to reproduce the experiments in any operating systems, Docker is required: [https://www.docker.com/](https://www.docker.com/).
Install it, and be sure that it is running when trying to reproduce the experiments.

To test if Docker is installed correctly:

- open the terminal;
- run ```docker run hello-world```.

***Expected output:***

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:7d246653d0511db2a6b2e0436cfd0e52ac8c066000264b3ce63331ac66dca625
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

# Reproducing the experiments

The instructions are valid for Unix-like systems (e.g., Linux Ubuntu, MacOS) and Windows (if using PowerShell).

1. Create the workspace

Open the terminal and type:

```
mkdir autoprep
cd autoprep
```

This simply creates a folder and goes into it.

2. Run the end-to-end experiments

In the same terminal window, run the docker image we published in this repository:

```
docker run -it --volume $(pwd):/home/autoprep ghcr.io/josephgiovanelli/autoprep:1.0.0
```

This mounts the above-created folder into the container, which is populated with code and results.

3. Run the experiments with intermediary results

In the same terminal window, you can run the docker image by leveraging our intermediary results:

```
docker run -it --volume $(pwd):/home/autoprep ghcr.io/josephgiovanelli/autoprep:1.0.0 -cache
```

The ```-cache``` flag allows to skip the optimization process (which would take roughly 2 months!).

3. Run the end-to-end experiments with a toy example

In the same terminal window, you can run a toy example:

```
docker run -it --volume $(pwd):/home/autoprep ghcr.io/josephgiovanelli/autoprep:1.0.0 -toy
```

The ```-toy``` flag allows to test the end-to-end process but with less datasets and time budget.

4. Extend the experiments

In the ```resources``` folder, you can edit the ```ext.json``` file to extend the included datasets by easily adding their OpenML IDS in the ```extra`` field:

```
{
    "default": [3, 6, 11, 12, 14, 15, 16, 18, 22, 23, 28, 29, 31, 32, 37, 44, 46, 50, 54, 151, 182, 188, 38, 307, 300, 458, 469, 554, 1049, 1050, 1053, 1063, 1067, 1068, 1590, 4134, 1510, 1489, 1494, 1497, 1501, 1480, 1485, 1486, 1487, 1468, 1475, 1462, 1464, 4534, 6332, 1461, 4538, 1478, 23381, 40499, 
    40668, 40966, 40982, 40994, 40983, 40975, 40984, 40979, 40996, 41027, 23517, 40923, 40927, 40978, 
    40670, 40701, 41145, 41156, 41157, 4541, 41158, 42742, 40498, 42734, 41162, 42733, 42732, 1596, 40981, 40685, 4135, 41142, 41161, 41159, 41163, 41164, 41138, 41143, 41146, 41150, 40900, 41165, 41166, 41168, 41169, 41147, 1111, 1169, 41167, 41144, 1515, 1457, 181, 10, 20, 26],
    "extra": [61]
}
```

This will allow the framework to download the dataset and include it along with the ```default`` ones.