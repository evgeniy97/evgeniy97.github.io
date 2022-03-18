# Philosophy of Project Gen42

Wee use rest api similar architecture to create our module. It means that each sub-module of our system can be used regardless of the others - it also give some flexibility in development of project.

Bse on our experience we divided module into four submodules: data generation, neural netwokrs, visualization and utilities.
Each of submodules can share data with another as far as we try to comply with contracts. Anyway, we donot want to make contracts strict as we believe that it is not the best practice for sceintific code to be extremly strict and spend resources just to check data. We think about adding data format check function in future, it will depend on how will the functionality be in demand.