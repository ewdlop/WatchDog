import random

# Define possible DNA sequences (antivirus signature)
DNA_BASES = ["A", "T", "C", "G"]  # Represents different detection mechanisms

class Antivirus:
    def __init__(self, signature=None, mutation_rate=0.1):
        """Initialize antivirus with a random or given signature."""
        self.signature = signature or self.generate_random_signature()
        self.mutation_rate = mutation_rate

    def generate_random_signature(self, length=10):
        """Generates a random DNA sequence as an antivirus signature."""
        return ''.join(random.choices(DNA_BASES, k=length))

    def mutate(self):
        """Apply genetic mutation to antivirus signature."""
        mutated_signature = list(self.signature)
        for i in range(len(mutated_signature)):
            if random.random() < self.mutation_rate:
                mutated_signature[i] = random.choice(DNA_BASES)
        self.signature = ''.join(mutated_signature)
        return self.signature

    def detect_malware(self, malware_dna):
        """Scoring mechanism: Higher matches mean better antivirus effectiveness."""
        match_count = sum(1 for a, m in zip(self.signature, malware_dna) if a == m)
        return match_count / len(malware_dna)  # Percentage match

    def display_info(self):
        """Display antivirus properties."""
        print(f"Antivirus Signature: {self.signature}")

# Malware DNA samples (Simulating different strains)
malware_samples = [
    "ATGCGTAGCA",  # Known variant
    "TGCATGCGAT",  # Evolved variant
    "CGTAGCTGCA"   # More mutated variant
]

# Create an initial antivirus
antivirus = Antivirus()
print("\n🔬 Initial Antivirus Signature:")
antivirus.display_info()

# Simulate 10 generations of antivirus evolution
for generation in range(10):
    print(f"\n🔄 Generation {generation + 1}:")
    antivirus.mutate()
    antivirus.display_info()
    
    # Test effectiveness against malware
    for i, malware in enumerate(malware_samples):
        effectiveness = antivirus.detect_malware(malware)
        print(f"  🦠 Malware {i+1} Detection Rate: {effectiveness * 100:.2f}%")

print("\n✅ Evolution Complete: Final Antivirus Signature Adapted.")
