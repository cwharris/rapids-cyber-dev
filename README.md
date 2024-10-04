# Dev Container for CUDF + MRC 24.10

## CAUTION:
Doing this will create sister-directories (`../.conda`, `../cudf`, `../mrc`, etc), so for tidiness you may want to keep this repository in an empty parent directory.

## Running the Dev Container:
Install VSCode extension `ms-vscode-remote.remote-containers` using `ctrl-shift-x`.

Open this repo as the workspace root.

`ctrl-shift-p`, and type/select `Dev Containers: ...` (replace `...` with whatever looks like `launch`/`build`) - hit enter.

Wait for the devcontainer to launch, and follow prompts regarding logging in with github. If you see warnings/errors regarding vault access, you may need to be added to the `rapidsai` and/or `nvidia` orgs on github.

## Cloning Repositories and Apply Patches
Once the container is booted, open a new terminal (in the vscode window, so it's inside the container), and run:

```
clone-all
```

Cloning should succeed, but the env solve might fail due to minor discrepencies. Fix that with a patch to cudf and mrc:
```
git -C ~/cudf apply ~/cyber-dev/.patches/cudf.patch
git -C ~/mrc apply ~/cyber-dev/.patches/mrc.patch
```

Re-run environment solve, which should now succeed:
```
rapids-make-conda-env
```

In case the conda environment didn't get automatically activated (due to bad solve on first try), activate it now:
```
conda activate cyber
```

## Building CUDF and MRC
Build everything:
```
build-all
```


## Check CUDF and MRC were built and installed
Once that's done (may take a while), you can try importing cudf/mrc:
```
python -c "import cudf"
python -c "import mrc"
```

If no errors appear, everything worked as intended.
