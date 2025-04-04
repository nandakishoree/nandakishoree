class FIND_S:
    def __init__(self, attributes, target_concept):
        self.attributes = attributes
        self.target_concept = target_concept
        self.msh = self.initialize_msh()

    def initialize_msh(self):
        msh = {}
        for attribute in self.attributes:
            msh[attribute] = '*'
        return msh

    def specialize_msh(self, sample):
        for attribute, value in sample.items():
            if self.msh[attribute] == '*' and value != self.target_concept:
                self.msh[attribute] = value

    def find_s(self, training_data):
        for sample in training_data:
            self.specialize_msh(sample)
        return self.msh

Example usage:
attributes = ['has_fur', 'has_wings', 'is_carnivore']
target_concept = 'mammal'
training_data = [
    {'has_fur': 'yes', 'has_wings': 'no', 'is_carnivore': 'no', 'mammal': 'yes'},
    {'has_fur': 'yes', 'has_wings': 'no', 'is_carnivore': 'yes', 'mammal': 'yes'},
    {'has_fur': 'no', 'has_wings': 'yes', 'is_carnivore': 'no', 'mammal': 'no'},
    {'has_fur': 'yes', 'has_wings': 'no', 'is_carnivore': 'no', 'mammal': 'yes'}
]

find_s = FIND_S(attributes, target_concept)
msh = find_s.find_s(training_data)
print("Most Specific Hypothesis (MSH):")
for attribute, value in msh.items():
    print(f"{attribute}: {value}")
