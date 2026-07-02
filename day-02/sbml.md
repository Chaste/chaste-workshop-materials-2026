# Hands-on session: SBML

In this session, you'll import a model written in [SBML](https://sbml.org/) (the Systems Biology Markup Language) from the [BioModels](https://www.ebi.ac.uk/biomodels/) repository and run it inside a Chaste project. This is a hands-on introduction to the SBML support in Chaste, which uses [`chaste-codegen-sbml`](https://github.com/Chaste/chaste-codegen-sbml) to turn an SBML model into C++ code you can build and simulate.


## Creating your SBML project

User projects live in the `projects` directory of the Chaste source tree. You'll create one from the project template with SBML support switched on.

1. Change into the `projects` directory:
   ```sh
   cd projects
   ```
2. Clone the [project template](https://github.com/Chaste/template_project) and switch to the `workshop-2026` branch:
   ```sh
   git clone -b workshop-2026 https://github.com/Chaste/template_project.git
   ```
3. Rename the folder to something meaningful, e.g. `SbmlExploration`:
   ```sh
   mv template_project SbmlExploration
   ```
4. Run the setup script and answer **yes** when it asks whether you want to create an **SBML** user project. You can answer **no** to the question about Python bindings for this session.
   ```sh
   cd SbmlExploration
   python setup_project.py
   ```

This creates a project with the SBML base classes in `src/`, and `chaste-codegen-sbml` installed into a local virtual environment (`.virtualenv/`).

## Importing and running the example model

Follow the steps in [`examples/goldbeter_1991`](https://github.com/Chaste/template_project/tree/workshop-2026/examples/goldbeter_1991) to import the [Goldbeter 1991 mitotic oscillator](https://www.ebi.ac.uk/biomodels/BIOMD0000000003) (`BIOMD0000000003`) from BioModels.


> [!NOTE]
> There are convenience scripts in the template to help with building the code. For example:
   ```sh
   scripts/configure.sh
   NCORES=16 scripts/compile.sh
   scripts/test.sh
   ```
> [!TIP]
> The first `compile.sh` can take a while. Subsequent builds are much faster because only your changes are recompiled. Set `NCORES` to the number of cpu cores in your codespace for a faster build.

## Next steps

- Browse the [BioModels repository](https://www.ebi.ac.uk/biomodels/) for another model that interests you.
- Import it into your project, run it, and produce some outputs. The workflow is the same as above — copy or download the SBML file (giving it a C++-friendly name), run `chaste_codegen_sbml` on it, write a short test, and build.
- `chaste_codegen_sbml` supports different `--model-type` values (`generic`, `srn`, or `cell-cycle`); try picking the one that best matches how you'd like to use the model.

## Feedback

- This feature is currently under testing and your feedback would be very welcome.
- Please add feedback in the [shared feedback document](https://docs.google.com/document/d/1zzn0G0qbTOmT5Ze3AlRsopvOJLxON4jyF9pXlWCcPgA/edit?usp=sharing) for this session: .
- Alternatively, create an issue directly on the [`chaste-codegen-sbml`](https://github.com/Chaste/chaste-codegen-sbml/issues) repository.
