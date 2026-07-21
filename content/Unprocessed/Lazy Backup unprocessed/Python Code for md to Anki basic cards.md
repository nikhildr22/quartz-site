```python

# Online Python - IDE, Editor, Compiler, Interpreter
# Initialize the string variable with the contents of the file
text = """

"""

# Split the string into a list of lines
lines = text.split('\n')

# Find the indices of all lines that start with "# "
indices = [i for i, line in enumerate(lines) if line.strip().startswith("# ")]

# Insert "START\nBasic\n" before each line starting with "# "
for i in indices:
    lines[i]="ENDanki\n\nSTARTanki\nBasic\n"+lines[i]+"\nBack:\n"
    # print(lines[i])
    # lines.insert(i, "END\n\nSTART\nBasic\n")
    # print(lines)
    # input()

# Join the modified lines back into a single string
modified_text = '\n'.join(lines)
modified_text+="\nENDanki"

# Print the modified text
print(modified_text)

```