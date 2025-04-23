# Detect React Code Smells

This GitHub Action detects code smells in React projects using [ReactSniffer](https://github.com/fabiosferreira/reactsniffer).

By default, it scans your project and generates two CSV reports bundled into a single artifact:

- `components_smells.csv`: Detected code smells in React components
- `files_smells.csv`: Contains only **Large File** smells

Additionally, this action can **block builds** if specific code smell thresholds are exceeded. You can configure thresholds via inputs (see below for examples).

## Supported Smells

ReactSniffer supported smells (from ReactSniffer repository description):

| Smell                              | Description                                                     |
| ---------------------------------- | --------------------------------------------------------------- |
| Large Component                    | Component with too many props, attributes, and/or lines of code |
| Too Many Props                     | Passing too many properties to a single component               |
| Inheritance Instead of Composition | Using inheritance to reuse code among components                |
| Props in Initial State             | Initializing state with props                                   |
| Direct DOM Manipulation            | Manipulating DOM directly                                       |
| Force Update                       | Forcing the component or page to update                         |
| JSX outside the render method      | Implementing markup in multiple methods                         |
| Uncontrolled Components            | A component that does not use props/state to handle form's data |
| Large File                         | A file with several components and lines of code                |

For more details about ReactSniffer you can check the official github repository in this [link](https://github.com/fabiosferreira/reactsniffer)

## Usage

### Basic

```yaml
- name: Detect React Code Smells
  uses: SocialSoftwareLivingLab/reactsniffer-action@1.0.0
```

This will run ReactSniffer and attach a CSV report artifact to the workflow.

### With Thresholds

**⚠️ Warning: Setting any threshold will cause the build to fail if that smell’s count exceeds the threshold.**

```yaml
- name: Detect React Code Smells
  uses: SocialSoftwareLivingLab/reactsniffer-action@1.0.0
  with:
    thresholds-large-component: 2
    thresholds-inheritance-instead-of-composition: 3
```

## Inputs

Each supported smell has its own threshold input:

| Name                                            | Default | Description                                             |
| ----------------------------------------------- | ------- | ------------------------------------------------------- |
| `thresholds-large-component`                    | `-1`    | Max allowed "Large Component" smells                    |
| `thresholds-too-many-props`                     | `-1`    | Max allowed "Too Many Props" smells                     |
| `thresholds-inheritance-instead-of-composition` | `-1`    | Max allowed "Inheritance Instead of Composition" smells |
| `thresholds-props-in-initial-state`             | `-1`    | Max allowed "Props in Initial State" smells             |
| `thresholds-direct-dom-manipulation`            | `-1`    | Max allowed "Direct DOM Manipulation" smells            |
| `thresholds-force-update`                       | `-1`    | Max allowed "Force Update" smells                       |
| `thresholds-jsx-outside-render-method`          | `-1`    | Max allowed "JSX Outside Render Method" smells          |
| `thresholds-uncontrolled-components`            | `-1`    | Max allowed "Uncontrolled Components" smells            |
| `thresholds-large-file`                         | `-1`    | Max allowed "Large File" smells                         |

> Use '-1' to ignore a smell threshold. Any other negative number is treated as 0, meaning no instances of that smell are allowed in the build.

## License

[MIT License](LICENSE)
