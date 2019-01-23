from gurobipy import *

# Input Problem Data
# Amount of edges in the graph
numE = 4 #south, north, west, ring
# Travel time slope
s = [-0.2, -5.5, -7.35, -0.71] #auslagern als funktion
# Maximum amount of cabins on each edge
amax = [35, 25, 21, 74]
# Minimum amount of cabins on each edge
amin = [14, 5, 4, 40]
# Travel time rnv
t_rnv = [12, 13.25, 9, 9.25, 25.5, 21.25, 18, 17.25]
tr = [12.625, 9.125, 23.375, 17.625]
# Minimum travel time shuttle
tmin = [7, 14.5, 14.9, 5.3]
# Maximum travel time shuttle
tmax  = [2.8, 3.5, 2.4, 2.9]
# Puffer travel time
z = [0,0,0,0]
# Cost per Edgepair
cedge = [6700000, 3534000, 3870000, 13290000]
# Cost per shuttle
c = 40000
# Budget
budget = 28000000


# The model
m = Model("Univercity-shuttle Project")

# Binary variables for the amount of shuttles
a = {}
for j in range(numE):
	a[j] = m.addVar(vtype=GRB.INTEGER, name="a%d" % j)

m.update()

# Constraint 1
for j in range(numE):
	m.addConstr(amax[j] - amin[j] >= a[j])

# Constraint 2
m.addConstr(quicksum((c*a[i]) + (amin[i]*c) + cedge[i] for i in range(numE)) <= budget)

# Constraint 3
for j in range(numE):
	m.addConstr(tr[j] + z[j] >= (a[j]*s[j]) + tmin[j])

m.setObjective(quicksum((s[j]*a[j]) for j in range(numE)), GRB.MINIMIZE)

m.optimize()

for i in range(len(a)):
	print(a[i])
