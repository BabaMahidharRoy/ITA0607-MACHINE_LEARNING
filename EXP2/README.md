##code
```
def candidate_elimination(data):
    num_features = len(data[0]) - 1

    # Initialize specific and general boundaries
    S = ['0'] * num_features
    G = [['?' for _ in range(num_features)]]

    for row in data:
        features, label = row[:-1], row[-1].lower()

        if label in ['yes', 'positive', '1']:
            # Initialize S with first positive example
            if S == ['0'] * num_features:
                S = list(features)
            else:
                for i in range(num_features):
                    if S[i] != features[i]:
                        S[i] = '?'
            # Prune G
            G = [g for g in G if all(g[i] == '?' or g[i] == S[i] for i in range(num_features))]

        else: # Negative example
            new_G = []
            for g in G:
                for i in range(num_features):
                    if g[i] == '?':
                        if S[i] != '?' and S[i] != features[i]:
                            hypothesis = g.copy()
                            hypothesis[i] = S[i]
                            new_G.append(hypothesis)
            G = new_G

    return S, G

dataset = [
    ['Sunny', 'Warm', 'Normal', 'Strong', 'Warm', 'Same', 'Yes'],
    ['Sunny', 'Warm', 'High', 'Strong', 'Warm', 'Same', 'Yes'],
    ['Rainy', 'Cold', 'High', 'Strong', 'Warm', 'Change', 'No'],
    ['Sunny', 'Warm', 'High', 'Strong', 'Cool', 'Change', 'Yes']
]
```
##ouput
```
Specific Boundary (S): ['Sunny', 'Warm', '?', 'Strong', '?', '?']
General Boundary (G): [['Sunny', '?', '?', '?', '?', '?'], ['?', 'Warm', '?', '?', '?', '?']]

specific_boundary, general_boundary = candidate_elimination(dataset)
print("Specific Boundary (S):", specific_boundary)
print("General Boundary (G):", general_boundary)
```

