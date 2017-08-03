
https://docs.continuum.io/anaconda-cloud/user-guide/getting-started#finding-downloading-and-installing-packages

Check conda version
```
conda --version
```

Update version
```
conda update conda
```

Create and activate an environment
```
conda create --name envname pandas
source activate envname

```
To change your path from the current environment back to the root:
```
source deactivate
```
Remove
```
conda remove --name flowers --all
```
List all environments created
```
conda info --envs
```
List packages under conda
```
conda list
```






Remove conda

```
conda install anaconda-clean
anaconda-clean --yes
rm -rf ~/anaconda

```
