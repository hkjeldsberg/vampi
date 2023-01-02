::: title
Installation
:::

# Installation

The Vascular Modeling Pypeline (VaMPy) is a collection of scripts used
to prepare, run, and analyze cardiac and atrial morphologies. This
includes pre-processing scripts for meshing and probe sampling, a
[Oasis](https://github.com/mikaem/Oasis) problem file for simulating
flow in the [internal carotid
artery](https://en.wikipedia.org/wiki/Internal_carotid_artery), and a
variety of post-processing scripts for computing WSS-based metrics, more
advanced turbulence metrics, and a variety of morphological parameters
in patient-specific geometries. The project is accessible through
[GitHub](https://github.com/KVSlab/VaMPy).

## Dependencies

The main dependencies of VaMPy are

-   morphMan
-   Oasis (FEniCS)
-   Paramiko

You can choose how to install the dependencies, but the fastest way to
get started is to install the dependencies through
[conda-forge]{.title-ref}. Start by installing [conda]{.title-ref}, by
downloading and installing
[Anaconda](https://www.anaconda.com/products/distribution) or
[Miniconda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)
on your computer.

## Installing morphMan and FEniCS

The [morphMan](https://github.com/KVSlab/morphMan) software can be
installed on all operative systems through Anaconda or
[conda-forge]{.title-ref}. Similarly, the
[FEniCS](https://fenicsproject.org/) software is also available through
Anaconda. Note that Windows users may need to install FEniCS as
described [here](https://fenicsproject.org/download/). To create a conda
environment with both software\'s installed, start by adding the
[conda-forge]{.title-ref} channel with:

``` console
$ conda config --add channels conda-forge
$ conda config --set channel_priority strict
```

Once the [conda-forge]{.title-ref} channel has been added, you can
create a [conda]{.title-ref} environment with [morphMan]{.title-ref} and
[FEniCS]{.title-ref} installed with:

``` console
$ conda create -n your_environment morphman fenics paramiko
```

::: note
::: title
Note
:::

Replace `your_environment` with the environment name.
:::

This will also install the minor dependency to [paramiko]{.title-ref}.
You can now activate your environment by running:

``` console
$ conda activate your_environment
```

or:

``` console
$ source activate your_environment
```

::: warning
::: title
Warning
:::

Some users may experience errors regarding compatibility if Anaconda
already has been configured with certain channels. To resolve this issue
you can remove conflicting channels using:

``` console
$ conda config --remove channels [CHANNEL NAME]
```

Alternatively, you set your Anaconda channel priority to *flexible*,
with the following command:

``` console
$ conda config --set channel_priority flexible
```
:::

::: warning
::: title
Warning
:::

After installing [morphMan]{.title-ref}, you may experience an error
during pre-processing, when the `.vtu` mesh is converted and compressed
into `.xml.gz` format using the `vmtkMeshWriter` method. As a temporary
fix you will need to update the `vmtkMeshWriter` script manually to
avoid this error, located at
`/Users/[USERNAME]/miniconda3/envs/your_environment/lib/python3.10/site-packages/vmtk/vmtkmeshwriter.py`.
To apply the fix, open the `vmtkmeshwriter.py` file, navigate to [line
264]{.title-ref}, and change:

file = open(self.OutputFileName,\'r\')

to:

file = open(self.OutputFileName,\'rb\').
:::

## Installing Oasis

The next step is to download and install
[Oasis](https://github.com/mikaem/Oasis) on your machine. Inside your
conda environment run the following commands to clone and install Oasis,
and the minor dependency to \`cppimport\`:

``` console
$ git clone https://github.com/mikaem/Oasis
$ pip install cppimport
$ pip install --editable Oasis
```

The `--editable` flag installs the project in editable mode meaning that
any changes to the original package will be reflected directly in your
environment.

## Downloading VaMPy

All that is left is to clone the [VaMPy]{.title-ref} repository:

``` console
$ git clone https://github.com/KVSLab/VaMPy.git
$ cd VaMPy
```

Now you are all set, and can start using the Vascular Modeling Pypeline.
