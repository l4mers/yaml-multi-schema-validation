# yaml-multi-schema-validation

## Initial Setup:
1. **Repository Setup**: Create a new GitHub repository named yaml-multi-schema-validation.
2. **GitHub Action Setup**: Within your repository, navigate to the "Actions" tab and set up a new
workflow. Use the "Set up a workflow yourself" option if prompted.
3. **Workflow Creation**: In the provided .yml file editor, use the GitHub Action setup:

```
name: Validate Multiple YAML Files

on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - run: npm install -g yaml-schema-validator

    - name: Validate Car YAML
      run: |
        schema validate -e -f car.yml -s schemas/schema_car.yml

    - name: Validate Computer YAML
      run: |
        schema validate -e -f computer.yml -s schemas/schema_computer.yml

    - name: Validate Person YAML
      run: |
        schema validate -e -f person.yml -s schemas/schema_person.yml

    - name: Validate Schedule YAML
      run: |
        schema validate -e -f schedule.yml -s schemas/schema_schedule.yml
```

4. **Add the Schemas**: Create a folder named schemas in the root of your repository. Inside schemas,
add the four schema files named schema_car.yml, schema_computer.yml,
schema_person.yml, and schema_schedule.yml. Copy the files from the yaml folder in
lesson_2.
5. **Initial YAML Creation**: In the root of your repository, add the four files named car.yml,
computer.yml, person.yml, and schedule.yml. Copy the files from the yaml folder in lesson_2.

### YAML Format Descriptions:
**Car**:
Requires a nested map for the manufacturer with a scalar string for the manufacturer's
name.
Scalars for model, year, and reg.
A sequence of scalar strings for attributes.

**Computer**:
Requires nested maps for cpu, memory, and disk.
For each component (e.g., cpu, memory, disk), you need further scalars or nested maps
describing the component attributes.

**Person**:
Requires a nested map for name with scalar strings for the first and last name.
Scalars for age, class, and start_year.
A sequence of scalar strings for hobbies.

**Schedule**:
Scalar for year and program.
A sequence for lessons, each having a nested map with scalars for date, startTime,
endTime, and description.

### The Exercise:
1. **Understanding the Requirements**: Using the provided schema and the above YAML format
descriptions, understand the required structure and data types for each of the YAML files.

2. **Craft the YAML**: Without referring directly to the schemas, create a representation in the respective
YAML files based on your understanding.

3. **Push and Observe**: After crafting your YAML, push your changes to GitHub and navigate to the
"Actions" tab. If the GitHub Action indicates a failure, it means one or more of your YAML files don't
fulfill the schema requirements.

4. **Iterative Refinement**: Review the logs from the GitHub Action to identify where your YAML might be
misaligned with the schema requirements. Update the necessary YAML files, push your changes, and
observe the results. Keep iterating until all YAML files are successfully validated.
