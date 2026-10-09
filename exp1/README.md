#EXP1
##CPDE
```
dfgbhnjm,.asxc vz import csv

def find_s(data):
    # Initialize hypothesis with the first positive example
    hypothesis = None
    for row in data:
        if row[-1].lower() in ['yes', 'positive', '1']:
            hypothesis = row[:-1].copy()
            break

    # Generalize with subsequent positive examples
    for row in data:
        if row[-1].lower() in ['yes', 'positive', '1']:
            for i in range(len(hypothesis)):
                if hypothesis[i] != row[i]:
                    hypothesis[i] = '?'
    return hypothesis

# Sample Data: [Sky, AirTemp, Humidity, Wind, Water, Forecast, EnjoySport]
dataset = [
    ['Sunny', 'Warm', 'Normal', 'Strong', 'Warm', 'Same', 'Yes'],
    ['Sunny', 'Warm', 'High', 'Strong', 'Warm', 'Same', 'Yes'],
    ['Rainy', 'Cold', 'High', 'Strong', 'Warm', 'Change', 'No'],
    ['Sunny', 'Warm', 'High', 'Strong', 'Cool', 'Change', 'Yes']
]

print("Most Specific Hypothesis:", find_s(dataset))
```
...
## OUTPUT
Most Specific Hypothesis: ['Sunny', 'Warm', '?', 'Strong', '?', '?']
