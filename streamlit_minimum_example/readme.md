
## Streamlit Minimum Example

Credit to Mark Sellors for the code. 

This is a streamlit example with minimal lines of code and minimal dependencies for an example to deploy to the hosting system of your choice. This could be useful when validating setup on the server, or for debugging an environment, or other scenarios. 

## Setup

From JupyterLab open a new Python script. 

Save the following as `app.py`: 

```
import streamlit as st

st.title("Hello World!")
```

Test that it runs with: 

```
streamlit run <app-name>/streamlit_app.py
```

For example: 

```
streamlit run ~/Projects/streamlit_min/app.py
```

When done the command to close the preview is `ctrl c`. 

## Deploy to Connect

Log in to your Connect instance and create an API key, following the instructions [here](https://docs.rstudio.com/how-to-guides/rsc/publish-jupyter-notebook/#step-3-connect-jupyter-notebook-to-rstudio-connect). 

You will also want to know your Connect server address. For example `https://colorado.rstudio.com/rsc/`. 

You will need to install the [rsconnect-python package](https://github.com/rstudio/rsconnect-python): 

```
pip install rsconnect-python
```

You might also need to install the jupyter package, as well as any other packages your code depends on: 

```
pip install rsconnect_jupyter
```

Save your server address using the [rsconnect-python package](https://github.com/rstudio/rsconnect-python): 

```
rsconnect add \
    --api-key my-api-key \
    --server https://connect.example.org:3939 \
    --name myserver
```

For example:

```
rsconnect add \
    --api-key **REDACTED** \
    --server https://colorado.rstudio.com/rsc/ \
    --name colorado
```

Create the requirements file: 

```
rsconnect write-manifest streamlit ~/Projects/streamlit_min/
```

If you are running into deploy issues where there are breaking packages you can edit the requirements file explicitly: 

```
# requirements.txt generated by rsconnect-python on 2022-09-21 14:59:58.865441
streamlit==1.11.0
```

Deploy it: 

```
rsconnect deploy streamlit -n <saved server name> --entrypoint main.py ...
```

For example: 

```
rsconnect deploy streamlit -n colorado --entrypoint app.py ~/Projects/streamlit_min/
```


We can also write the requirements.txt file using pip: 

```
pip freeze > requirements.txt
```


## Other references 

Resources: 

 - Discussion on Jupyter and kernels: [https://solutions.rstudio.com/python/jupyter/](https://solutions.rstudio.com/python/jupyter/)
 - Python and installating packages: [https://solutions.rstudio.com/python/minimum-viable-python/installing-packages/](https://solutions.rstudio.com/python/minimum-viable-python/installing-packages/)
 - The Connect documentaiton on deploying streamlit to Connect: [https://docs.rstudio.com/connect/user/streamlit/](https://docs.rstudio.com/connect/user/streamlit/)
 - Demo content: [https://github.com/sol-eng/python-examples](https://github.com/sol-eng/python-examples) 
 - Publishing from the command line: [https://docs.rstudio.com/connect/user/publishing-cli/](https://docs.rstudio.com/connect/user/publishing-cli/) 
 - The page on the resconnect package explains saving the server: [https://github.com/rstudio/rsconnect-python](https://github.com/rstudio/rsconnect-python) or [https://pypi.org/project/rsconnect-python/](https://pypi.org/project/rsconnect-python/) 







