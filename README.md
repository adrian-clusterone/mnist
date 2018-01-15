# MNIST on ClusterOne
<p align="center">
<img src="c1_logo.png" alt="ClusterOne" width="200">
<br>
<br>
<a href="https://slackin-altdyjrdgq.now.sh"><img src="https://slackin-altdyjrdgq.now.sh/badge.svg" alt="join us on slack"></a>
</p>

This is a demo to show you how to run a handwritten digit recognition model on [ClusterOne](https://clusterone.com). The demo uses [TensorFlow](https://tensorflow.org) and the [MNIST](http://yann.lecun.com/exdb/mnist/) dataset.



Follow the instructions below to run the model on ClusterOne using the just command line interface. For an in-depth tutorial based on this repository, check out the [ClusterOne documentation](https://docs.clusterone.com/v1.0/docs/mnist-with-clusterone).

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [More Info](#more-info)
- [License](#license)

## Install

To run this project, you need:

- [Python](https://python.org/) 3.5 or higher
- [Git](https://git-scm.com/)
- The ClusterOne Python library. Install it with `pip install clusterone`
- TensorFlow 1.0.0 or higher. Install it with `pip install tensorflow`
- A ClusterOne account. [Sign up](https://clusterone.com/) for free if you don't have an account yet.

### Setting Up

Start out by cloning this repository onto your local machine. 

Then, navigate to the folder you cloned into and open [mnist.py](mnist.py). Find the variables `PATH_TO_LOCAL_LOGS` and `ROOT_PATH_TO_LOCAL_DATA`. Change the paths to where you want log files and data to be saved on your local machine. 

The default is `~/Documents/mnist/logs` for log files and `~/Documents/data/mnist` for the data. Make sure Python has permission to write in the folders you choose.

That's it, you're all set up!

## Usage

In this example, we use the just command line tool. It comes with the ClusterOne Python library and is installed automatically with the library.

Start by opening a command line and logging into your ClusterOne account using `just login`.

### Run locally as one-layer network

Now, run the demo as a simple one-layer network:

```bash
$ python mnist.py
```

The program will download the MNIST dataset automatically into the data location you specified during setup. Once the network starts training, you should see loss values appear in the console.

### Run on ClusterOne

Instead of on your local machine, you can also run the program online on the ClusterOne platform.

First, create a new project on ClusterOne:

```shell
$ just create project --name <PROJECT_NAME>
```

Then, upload the code to the new project:

```shell
$ git push clusterone master
```

Finally, create a job and run it. Make sure to replace `YOUR_USERNAME` and `PROJECT_NAME` with your username and the name of your ClusterOne project.

```shell
$ just run --project <YOUR_USERNAME>/<PROJECT_NAME> \ 
--module mnist --requirements requirements.txt --framework-version 1.0.0 \
--mode distributed --worker-replicas 2 --worker-type p2.xlarge \
--ps-replicas 1 --ps-type c4.2xlarge \
--time-limit 1h --description ""
```

The job will start automatically. You can monitor its progress on the command line using `just pulse`. More elaborate monitoring is available on the [Matrix](https://clusterone.com/matrix), ClusterOne's graphical web interface. 

## More Info

For further information on this example, take a look at the tutorial based on this repository in the [ClusterOne Documentation](https://docs.clusterone.com/v1.0/docs/mnist-with-clusterone).

For further info on the MNIST dataset, check out [Yann LeCun's page](http://yann.lecun.com/exdb/mnist/) about it. To learn more about TensorFlow and Deep Learning in general, take a look at the [TensorFlow](https://tensorflow.org) website.

## License

[MIT](LICENSE) © ClusterOne Inc.

The [MNIST](http://yann.lecun.com/exdb/mnist/) dataset has been created and curated by Corinna Cortes, Christopher J.C. Burges, and Yann LeCun.