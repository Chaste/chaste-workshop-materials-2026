# Hands-on session: Creating Python bindings

In this session, you'll write C++ code in a Chaste project, create Python bindings for it, and use your class from a Python script.


## Creating your project

User projects live in the `projects` directory of the Chaste source tree. You'll create one from the project template with Python bindings switched on.

1. Change into the `projects` directory:
   ```sh
   cd projects
   ```
2. Clone the [project template](https://github.com/Chaste/template_project) and switch to the `workshop-2026` branch:
   ```sh
   git clone -b workshop-2026 https://github.com/Chaste/template_project.git
   ```
3. Rename the folder to something meaningful, e.g. `WrapperExample`:
   ```sh
   mv template_project WrapperExample
   ```
4. Run the setup script and answer **yes** when it asks whether you want to create **Python bindings**. You can answer **no** to the question about SBML for this session.
   ```sh
   cd WrapperExample
   python setup_project.py
   ```

This creates a project set up to generate Python bindings, with the [cppwg](https://github.com/Chaste/cppwg) configuration listing the classes to wrap in `dynamic/config.yaml`.

## Creating a class and its Python bindings

You'll create a new Force class, generate Python bindings for it, and use it in a Python script. Follow the walkthrough in the [`examples/my_force`](https://github.com/Chaste/template_project/tree/workshop-2026/examples/my_force) directory of the template.

> [!TIP]
> There are convenience scripts in the project folder to help with building the code. For example, from the project folder:
>
> ```sh
> scripts/configure.sh          # do this the first time, or after adding new files/wrappers
> NCORES=16 scripts/compile.sh  # rebuild the project and bindings
> scripts/bindings_install.sh   # install the bindings into .virtualenv/
> ```
>
> The first `compile.sh` can take a while. Subsequent builds are much faster because only your changes are recompiled. Set `NCORES` to the number of cpu cores in your codespace for a faster build.

## Next steps

- Add another method to your Force class, or create a different class, and add it to `dynamic/config.yaml` the same way.
- Regenerate the wrappers and rebuild.
- Reinstall in the virtualenv and test your new class in Python.
