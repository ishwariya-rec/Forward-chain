# Forward-chain
# forward_chaining.py

def forward_chaining(rules, facts, goal):
    inferred = set(facts)
    applied_rules = set()

  while True:
        new_inferences = set()
        for i, rule in enumerate(rules):
            if i in applied_rules:
                continue
            head, body = rule
            if all(b in inferred for b in body):
                if head not in inferred:
                    new_inferences.add(head)
                applied_rules.add(i)
        
  if goal in inferred:
            return True

  if not new_inferences:
            return False

  inferred.update(new_inferences)

# --------- Knowledge Base ---------
rules = [
    ("cold", ["rainy"]),
    ("wear_jacket", ["cold"]),
    ("wet", ["rainy"]),
    ("rainy", ["cloudy", "humid"]),
    ("humid", ["summer"])
]

facts = ["cloudy", "summer"]

# --------- Query ---------
goal = "wear_jacket"
result = forward_chaining(rules, facts, goal)

print(f"Can we infer '{goal}'? {'Yes' if result else 'No'}")
