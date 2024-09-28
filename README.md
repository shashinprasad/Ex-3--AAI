<H3>ENTER YOUR NAME : Shashin prasad S</H3>
<H3>ENTER YOUR REGISTER NO : 212222230144</H3>
<H3>EX. NO : 3</H3>
<H3>DATE : 08-09-2024</H3>
<H1 ALIGN =CENTER> Implementation of Approximate Inference in Bayesian Networks
</H1>

## Aim :

To construct a python program to implement approximate inference using Gibbs Sampling.</br>

## ALGORITHM :

### STEP 1 :

Bayesian Network Definition and CPDs:<br>
<ul> <li>Define the Bayesian network structure using the Bayesian Network class from pgmpy.models.</li>
<li>Define Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class.</li>
<li>Add the CPDs to the network.</li></ul>

### STEP 2 :

Printing Bayesian Network Structure:<br>
<ul><li>Print the structure of the Bayesian network using the print(network) statement.</li></ul>

### STEP 3 :

Graph Visualization:
<ul><li>Import the necessary libraries (networkx and matplotlib).</li>
<li>Create a directed graph using networkx.DiGraph().</li>
<li>Define the nodes and edges of the graph.</li>
<li>Add nodes and edges to the graph.</li>
<li>Optionally, define positions for the nodes.</li>
<li>Use nx.draw() to visualize the graph using matplotlib.</li></ul>

### STEP 4 :

Gibbs Sampling and MCMC:<br>
<ul><li>Initialize Gibbs Sampling for MCMC using the GibbsSampling class and provide the Bayesian network.</li>
<li>Set the number of samples to be generated using num_samples.</li></ul>

### STEP 5 :

Perform MCMC Sampling:<br>
<ul><li>Use the sample() method of the GibbsSampling instance to perform MCMC sampling.</li>
<li>Store the generated samples in the sample's variable.</li></ul>

### STEP 6 :

Approximate Probability Calculation:<br>
<ul><li>Specify the variable for which you want to calculate the approximate probabilities (query_variable).</li>
<li>Use .value_counts(normalize=True) on the samples of the query_variable to calculate approximate probabilities.</li></ul>

### STEP 7 :

Print Approximate Probabilities:<br>
<ul><li>Print the calculated approximate probabilities for the specified query_variable.</li></ul>

## Program :

```
!pip install pgmpy
!pip install networkx
from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.sampling import GibbsSampling
import networkx as nx
import matplotlib.pyplot as plt

alarm_model = BayesianNetwork(
    [
        ("Burglary", "Alarm"),
        ("Earthquake", "Alarm"),
        ("Alarm", "JohnCalls"),
        ("Alarm", "MaryCalls"),
    ]
)

# Defining the parameters using CPT
from pgmpy.factors.discrete import TabularCPD

cpd_burglary = TabularCPD(
    variable="Burglary", variable_card=2, values=[[0.999], [0.001]]
)
cpd_earthquake = TabularCPD(
    variable="Earthquake", variable_card=2, values=[[0.998], [0.002]]
)
cpd_alarm = TabularCPD(
    variable="Alarm",
    variable_card=2,
    values=[[0.999, 0.71, 0.06, 0.05], [0.001, 0.29, 0.94, 0.95]],
    evidence=["Burglary", "Earthquake"],
    evidence_card=[2, 2],
)
cpd_johncalls = TabularCPD(
    variable="JohnCalls",
    variable_card=2,
    values=[[0.95, 0.1], [0.05, 0.9]],
    evidence=["Alarm"],
    evidence_card=[2],
)
cpd_marycalls = TabularCPD(
    variable="MaryCalls",
    variable_card=2,
    values=[[0.1, 0.7], [0.9, 0.3]],
    evidence=["Alarm"],
    evidence_card=[2],
)

# Associating the parameters with the model structure
alarm_model.add_cpds(
    cpd_burglary, cpd_earthquake, cpd_alarm, cpd_johncalls, cpd_marycalls
)
print("Bayesian Network Structure")
print(alarm_model)
G=nx.DiGraph()
nodes=['Burglary','Earthquake','JohnCalls','MaryCalls']
edges=[('Burglary','Alarm'),('Earthquake','Alarm'),('Alarm','JohnCalls'),('Alarm','MaryCalls')]

G.add_nodes_from(nodes)
G.add_edges_from(edges)
pos={
    'Burglary':(0,0),
    'Earthquake':(2,0),
    'Alarm':(1,-2),
    'JohnCalls':(0,-4),
    'MaryCalls':(2,-4)
    }
nx.draw(G,pos,with_labels=True,node_size=1500,node_color="skyblue",font_size=10,font_weight="bold",arrowsize=20)
plt.title("Bayesian Network: Burglar Alarm Problem")
plt.show()
```

## Output :

![Screenshot 2024-09-08 210634](https://github.com/user-attachments/assets/09602a4f-6caa-4551-a076-2a486813a138)

![Screenshot 2024-09-08 210645](https://github.com/user-attachments/assets/1f1a28a2-3fe0-4d89-adb4-76279ea4fa43)


## Result :

Thus, Gibb's Sampling( Approximate Inference method) is succuessfully implemented using python.
