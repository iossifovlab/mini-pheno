# Mini pheno repository

## Data provided
This example phenotype data repository contains the following data:
- Two instruments files with a total of five measures
- Pedigree with three quad families
- Two measure description files (one has alternative data for demonstration purposes)

Additionally, there is a full copy of the data in an example input dir (`example_input_dir`).
This copy is used to demonstrate the `input_dir` field in import configurations.


## Import configs provided

* `pheno_import_project_DEFAULT.yaml`
This is the default example import project. It uses the default input dir settings, which is to treat all paths in the import config relative to the directory it is located in.
A basic override of instrument configuration is shown by using a different delimiter for the second instrument.

* `pheno_import_project_INPUTDIR.yaml`
This import project is nearly identical to the default one, with the exception of manually setting the `input_dir` from which all other paths are considered relative to.

* `pheno_import_project_NONSTANDARD_DESCRIPTIONS.yaml`
This import project demonstrates various overrides in specifying data dictionaries (files to read measure descriptions from), as well as manual input of measure descriptions inside the project.

## Running the import

The commands below all produce output into a directory called `output`.
These commands also produce flag files (`*.flag`) - make sure to clean them up before running another import!

```bash
import_tools_pheno pheno_import_project_DEFAULT.yaml
```

```bash
import_tools_pheno pheno_import_project_INPUTDIR.yaml
```

```bash
import_tools_pheno pheno_import_project_NONSTANDARD_DESCRIPTIONS.yaml
```

## Building a phenotype browser DB

To build a phenotype browser DB, you need to follow these steps:
1. Run any import of your choice
2. Create a subdirectory of your choice, for example called "pheno"
3. Move the result of your phenotype import into this subdirectory. You should end up with something similar to `mini_pheno/pheno/output`. This is necessary in order to mimic the layout that the browser-building tool expects.
4. Run the following command:
   ```bash
   build_pheno_browser pheno --phenotype-data-id mini_pheno
   ```
5. `mini_pheno/pheno/output` should now contain a phenotype browser database file.
