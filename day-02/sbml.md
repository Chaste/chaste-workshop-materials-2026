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

You'll import the [Goldbeter 1991 mitotic oscillator](https://www.ebi.ac.uk/biomodels/BIOMD0000000003) (`BIOMD0000000003`) from BioModels and run it as a sub-cellular reaction network (SRN). The full walkthrough lives in the [`examples/goldbeter_1991`](https://github.com/Chaste/template_project/tree/workshop-2026/examples/goldbeter_1991) directory of the template.

1. Activate the project's virtual environment:
   ```sh
   source .virtualenv/bin/activate
   ```
2. Copy the example SBML model into the project root:
   ```sh
   cp examples/goldbeter_1991/Goldbeter1991.xml .
   ```
   > [!NOTE]
   > The file is named `Goldbeter1991.xml` (no spaces or dashes) so that valid C++ class names can be generated from it. If you download models yourself later, give them C++-friendly names.
3. Convert the SBML model into Chaste C++ code, writing the generated files into `src/`:
   ```sh
   chaste_codegen_sbml Goldbeter1991.xml --model-type srn --output-dir src/
   ```
   This generates the ODE system and SRN model classes (e.g. `Goldbeter1991SbmlOdeSystem.[hpp|cpp]` and `Goldbeter1991SbmlSrnModel.[hpp|cpp]`) in `src/`.
4. Add the test that exercises the model. Copy the provided test into your `test/` directory and register it in the test pack:
   ```sh
   cp examples/goldbeter_1991/TestGoldbeter1991SbmlSrnModel.hpp test/
   ```
   Then add the following line to `test/ContinuousTestPack.txt`:
   ```
   TestGoldbeter1991SbmlSrnModel.hpp
   ```
   The test builds a cell carrying the imported SRN model, integrates it to a steady state, and checks the resulting concentrations.
5. There are convenience scripts in the template to help with building the code. Configure, build and run the test:
   ```sh
   scripts/configure.sh
   NCORES=16 scripts/compile.sh
   scripts/test.sh
   ```
   > [!TIP]
   > The first `compile.sh` can take a while. Subsequent builds are much faster because only your changes are recompiled. Set `NCORES` to the number of cpu cores in your codespace for a faster build.

If everything worked, the test passes and the model reaches steady-state concentrations of approximately:

- `C` ≈ 0.547
- `M` ≈ 0.294
- `X` ≈ 0.0067

## Next steps

- Browse the [BioModels repository](https://www.ebi.ac.uk/biomodels/) for another model that interests you.
- Import it into your project, run it, and produce some outputs. The workflow is the same as above — copy or download the SBML file (giving it a C++-friendly name), run `chaste_codegen_sbml` on it, write a short test, and build.
- `chaste_codegen_sbml` supports different `--model-type` values (`generic`, `srn`, or `cell-cycle`); try picking the one that best matches how you'd like to use the model.

## Feedback

- This feature is currently under testing and your feedback would be very welcome.
- Please add feedback in the shared document for this session.
- Alternatively, create an issue directly on the [`chaste-codegen-sbml`](https://github.com/Chaste/chaste-codegen-sbml/issues) repository.
