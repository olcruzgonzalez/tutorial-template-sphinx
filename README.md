# Template for the Sphinx Tutorial

This repository serves as a background of my experience in following the tutorial ["Tutorial: Build your first project"](https://www.sphinx-doc.org/en/master/tutorial/index.html) from [Sphinx](https://www.sphinx-doc.org/en/master/index.html). The purpose is to summarize all the steps I took and the further tasks carried out along the way. The main goal is to provide the community with a complete tutorial-based template, as well as a useful starting point for deploying their own projects. To access the static documentation web page resulting from this tutorial, click  [here](https://olcruzgonzalez.github.io/tutorial-template-sphinx/).

Please, click on [Template](https://github.com/olcruzgonzalez/tutorial-template-sphinx/generate) for getting start and remember to update your `Personal access tokens`  within the file `sphinx.yml` (see **Deployment** section below).

## Steps Followed in the Tutorial

Below I present the tutorial items I have followed to obtain the template shown in this repository. Notice that I have only focused on the HTML format, Python object documentation and the deployment on GitHub.

- Getting started 
    * Setting up your project and development environment
    * Creating the documentation layout
- First steps to document your project using Sphinx
    * Building your HTML documentation
- More Sphinx customization
    * Enabling a built-in extension
    * Using a third-party HTML theme
- Narrative documentation in Sphinx
    * Structuring your documentation across multiple pages
    * Adding cross-references
- Describing code in Sphinx
    * Python
        * Documenting Python objects
        * Cross-referencing Python objects
        * Including doctests in your documentation
- Automatic documentation generation from code
    * Reusing signatures and docstrings with autodoc
    * Generating comprehensive API references
- Appendix: Deploying a Sphinx project online
    * Sphinx-friendly deployment options
    * Embracing the “Docs as Code” philosophy
    * Publishing your documentation sources
        * GitHub
    * Publishing your HTML documentation
        * GitHub Pages


## Insights on the Tutorial

The tutorial ["Tutorial: Build your first project"](https://www.sphinx-doc.org/en/master/tutorial/index.html) is very well written and easy to follow. I strongly recommend it to get an initial and complete understanding of this tool that is [Sphinx](https://www.sphinx-doc.org/en/master/index.html). You can use the [Template](https://github.com/olcruzgonzalez/tutorial-template-sphinx/generate) I share in this repository as a guide and verify that all the steps have been done. 

However, if you decide to go through the tutorial **from scratch**, these are some suggestions based on my experience in doing so:

###  List of dependencies and prerequisites

* Python installed on your system
* A text editor or IDE to open the source code
* A terminal or command prompt to run commands
* A Version Control System installed. Here, I have used [Git](https://git-scm.com/).

### Workflow in a Nutshell


1. Create a repository on GitHub, add README and LICENSE files.

2. Clone the repository in a local directory.

```
git clone https://github.com/username/RepositoryName.git
cd RepositoryName
```
3. Now, add the Python scripts for which you intend to create the documentation, for instance `lumanche.py`, and update the README file. 

4. Create and activate a virtual environment

```
python -m venv venv
```
* On Linux/macOS:
 
    ```
    source myenv/bin/activate
    ```
* On Windows: 

    ```
    myenv\Scripts\Activate.ps1
    ```

5. Install Sphinx
```
(venv) pip install sphinx 
```
	
6. Creating the documentation layout 
	
```
(venv) sphinx-quickstart docs
(venv) sphinx-build -b html docs/source/ docs/build/html
```

7. Perform any changes or customizations, see ["Tutorial: Build your first project"](https://www.sphinx-doc.org/en/master/tutorial/index.html) for more details. As an example, try a new theme, [furo](https://github.com/pradyunsg/furo):
```
(venv) pip install furo
```

docs/source/conf.py

    html_theme = 'furo'

8. Update the changes
```
(venv) sphinx-build -b html docs/source/ docs/build/html
```
or 
```
(venv) cd docs
(venv) make html
```

9. Commit and push to the remote repository
```
(venv) git add .
(venv) git commit -m "commit message"
(venv) git push origin local_branch_name
```

10. Deploying on GitHub pages


### Deployment 

When following the instructions in the tutorial, [Appendix: Deploying a Sphinx project online](https://www.sphinx-doc.org/en/master/tutorial/deploying.html), do as below:

* Use the command `freeze` and then update `requirements.txt` with all the modulus installed in your virtual environment.
```
pip freeze
```

* Before doing the push to the GitHub repository delete `docs/build` directory.

* Within the file `sphinx.yml`, update the information of your GitHub token. You must grant write access to the repository for Actions by using an access token (PAT). To do this, follow the steps:
    
    *  In GitHub, go to your profile settings and click on `Developer settings`.

    * Go to the `Personal access tokens` section and generate a new token.

    * Give the token a descriptive name and select the "repo" scope (`workflow`).

    * Store the token securely in your repository as a secret. That is:
        - Go to your GitHub repository where you are deploying your Sphinx project.
        - In the upper-right corner of the page, click on the `Settings` tab.
        - In the left sidebar, click on `Secrets and variables` and then `Actions`.
        - Click on the `New repository secret` button.
        - Enter a name for the secret. For example, "TUTORIAL_TEMPLATE_SPHINX_TOKEN".
        - Click on the `Add secret` button.
        
    * Modify the workflow file (.github/workflows/sphinx.yml) to use the personal access token as follows:

       
        ```
        name: Sphinx build

        on: push

        jobs:
        build:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/checkout@v3
            - name: Build HTML
            uses: ammaraskar/sphinx-action@master
            - name: Upload artifacts
            uses: actions/upload-artifact@v3
            with:
                name: html-docs
                path: docs/build/html/
            - name: Deploy
            uses: peaceiris/actions-gh-pages@v3
            if: github.ref == 'refs/heads/main'
            with:
                github_token: ${{ secrets.TUTORIAL_TEMPLATE_SPHINX_TOKEN }}
                publish_dir: docs/build/html
        ```


## License

The template is available as open source under the terms of the [MIT License](https://github.com/olcruzgonzalez/tutorial-template-sphinx/blob/main/LICENSE).

Please, feel free to [contact me](https://github.com/olcruzgonzalez) for any further information. I hope you find the repository useful.  





