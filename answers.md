# CMPS 2200 Assignment 4
## Answers

**Name:**______Darian Tocci___________________






- **1a.**
  Depth of a d‑ary heap: Θ(log_d n).

- **1b.**
  delete‑min: swaps downward → O(d · log_d n).
  insert: swaps upward → O(log_d n).


- **1c.**
  Using a d‑ary heap in Dijkstra:
|V| delete‑mins → |V| · d · log_d |V|
|E| decrease‑keys/inserts → |E| · log_d |V|
Total work: O(|V|·d·log_d|V| + |E|·log_d|V|).
- **1d.**
  If |E| = |V|^(1+ε), choose d = |V|^ε → running time becomes O(|E|).

- **2a.**
  For k = -1 no intermediate vertices, only direct edges:
APSP(0,0,-1) = 0
APSP(0,1,-1) = -2
APSP(0,2,-1) = 2
APSP(1,0,-1) = ∞
APSP(1,1,-1) = 0
APSP(1,2,-1) = 1
APSP(2,0,-1) = ∞
APSP(2,1,-1) = ∞
APSP(2,2,-1) = 0
For k = 0 can use vertex 0:
APSP(0,0,0) = 0
APSP(0,1,0) = -2
APSP(0,2,0) = 2
APSP(1,0,0) = ∞
APSP(1,1,0) = 0
APSP(1,2,0) = 1
APSP(2,0,0) = ∞
APSP(2,1,0) = ∞
APSP(2,2,0) = 0
For k = 1 can use vertices 0 and 1:
APSP(0,0,1) = 0
APSP(0,1,1) = -2
APSP(0,2,1) = -1 path 0→1→2 with cost -2+1=-1, better than direct edge with cost 2
APSP(1,0,1) = ∞
APSP(1,1,1) = 0
APSP(1,2,1) = 1
APSP(2,0,1) = ∞
APSP(2,1,1) = ∞
APSP(2,2,1) = 0
For k = 2 can use all vertices:
APSP(0,0,2) = 0
APSP(0,1,2) = -2
APSP(0,2,2) = -1
APSP(1,0,2) = 3 path 1→2→0 with cost 1+2=3
APSP(1,1,2) = 0
APSP(1,2,2) = 1
APSP(2,0,2) = ∞
APSP(2,1,2) = 0 path 2→0→1 with cost can't work... actually this stays ∞
APSP(2,2,2) = 0

- **2b.**
  Looking at the relationship, I can see that APSP(i,j,2) can be written as:
APSP(i,j,2) = min(APSP(i,j,1), APSP(i,2,1) + APSP(2,j,1))
For example, APSP(0,2,2) = min(APSP(0,2,1), APSP(0,2,1) + APSP(2,2,1)) = min(-1, -1+0) = -1
This means the shortest path either doesn't use vertex 2 or it does use vertex 2 as an intermediate vertex.

- **2c.**
  The optimal substructure property is:
APSP(i,j,k) = min(APSP(i,j,k-1), APSP(i,k,k-1) + APSP(k,j,k-1))
This works because the shortest path from i to j using vertices {0,1,...,k} either doesn't use vertex k at all (so it's just APSP(i,j,k-1)), or it does use vertex k, in which case we go from i to k and then from k to j, both using only vertices {0,1,...,k-1}.

- **2d.**
  Number of distinct subproblems:

i can be any of n vertices
j can be any of n vertices
k ranges from -1 to n-1, so n+1 values

Total subproblems = n × n × (n+1) = O(n³)
Each subproblem takes O(1) work to compute (just a min comparison and one addition).
Total work = O(n³)
- **2e.**
  Johnson's algorithm has work O(|V||E|log|E|)
Our DP algorithm has work O(n³) where n = |V|
The DP algorithm is preferable when the graph is dense (lots of edges). Specifically:

When |E| ≈ |V|², Johnson's algorithm is O(|V|³log|V|) while our DP is O(|V|³), so DP is faster by a logarithmic factor
The DP algorithm is simpler to implement and doesn't require graph transformations

Johnson's algorithm is preferable when the graph is sparse (few edges):

When |E| ≈ |V|, Johnson's is O(|V|²log|V|) which is much better than our O(|V|³)


- **3a.**
  MST is also optimal for MMET because MST minimizes the heaviest edge on every cut.

- **3b.**
  Algorithm for next‑best tree:
For each edge e not in the MST:
Add e to MST → creates a cycle.
Remove the largest edge in that cycle.
Compute weight of the resulting tree.
Take the minimum among these candidates

- **3c.**
  Work: computing all candidates is O(E log V) ,  each uses LCA / cycle max‑edge query.
