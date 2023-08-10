# Generator

[Shacl2md Index](../README.md#shacl2md-index) /
[Shacl2md](./index.md#shacl2md) /
Generator

> Auto-generated documentation for [shacl2md.generator](../../shacl2md/generator.py) module.

- [Generator](#generator)
  - [Generator](#generator-1)
    - [Generator().add_ontology_graph](#generator()add_ontology_graph)
    - [Generator().add_shacl_graphs](#generator()add_shacl_graphs)
    - [Generator().get_graph](#generator()get_graph)
  - [ShaclGraph](#shaclgraph)
    - [ShaclGraph().generate_md](#shaclgraph()generate_md)
    - [ShaclGraph().generate_puml](#shaclgraph()generate_puml)
    - [ShaclGraph().generate_vscode_snippet](#shaclgraph()generate_vscode_snippet)
    - [ShaclGraph().validate](#shaclgraph()validate)
  - [ShaclMarkdownGenerator](#shaclmarkdowngenerator)
    - [ShaclMarkdownGenerator().filter_graph](#shaclmarkdowngenerator()filter_graph)
    - [ShaclMarkdownGenerator().filter_language](#shaclmarkdowngenerator()filter_language)
    - [ShaclMarkdownGenerator().generate](#shaclmarkdowngenerator()generate)
  - [ShaclSnippetGenerator](#shaclsnippetgenerator)
    - [ShaclSnippetGenerator().generate](#shaclsnippetgenerator()generate)

## Generator

[Show source in generator.py:23](../../shacl2md/generator.py#L23)

#### Signature

```python
class Generator:
    def __init__(
        self,
        languages: List[str],
        output_dir: str = "./",
        shacl_shacl_validation: bool = False,
        ontology_graphs: List[Union[str, Graph]] = None,
        logger: Logger = None,
    ):
        ...
```

### Generator().add_ontology_graph

[Show source in generator.py:46](../../shacl2md/generator.py#L46)

Add an ontology graph.

#### Arguments

ontology_graph (str | Graph): Ontology graph to add.

#### Signature

```python
def add_ontology_graph(self, ontology_graph: Union[str, Graph]):
    ...
```

### Generator().add_shacl_graphs

[Show source in generator.py:69](../../shacl2md/generator.py#L69)

Add SHACL graphs.

#### Arguments

- `**shacls` - Dictionary of SHACL files or Graphs to generate documentation for. The key is the name of the SHACL graph, the value is the filename of the SHACL file.

#### Signature

```python
def add_shacl_graphs(self, **shacls):
    ...
```

### Generator().get_graph

[Show source in generator.py:60](../../shacl2md/generator.py#L60)

Get a graph by name.

#### Arguments

- `graph_name` *str* - Name of the graph to get.

#### Signature

```python
def get_graph(self, graph_name: str):
    ...
```



## ShaclGraph

[Show source in generator.py:250](../../shacl2md/generator.py#L250)

#### Signature

```python
class ShaclGraph:
    def __init__(
        self,
        name: str,
        lang: str,
        generator: Union[ShaclMarkdownGenerator, ShaclSnippetGenerator],
    ):
        ...
```

#### See also

- [ShaclMarkdownGenerator](#shaclmarkdowngenerator)
- [ShaclSnippetGenerator](#shaclsnippetgenerator)

### ShaclGraph().generate_md

[Show source in generator.py:318](../../shacl2md/generator.py#L318)

Generate markdown documentation from the SHACL graph.

#### Signature

```python
def generate_md(self):
    ...
```

### ShaclGraph().generate_puml

[Show source in generator.py:279](../../shacl2md/generator.py#L279)

Generate a PlantUML diagram from the SHACL graph.

#### Signature

```python
def generate_puml(self):
    ...
```

### ShaclGraph().generate_vscode_snippet

[Show source in generator.py:355](../../shacl2md/generator.py#L355)

Generate Snippets for triples in VSCODE

#### Signature

```python
def generate_vscode_snippet(self):
    ...
```

### ShaclGraph().validate

[Show source in generator.py:433](../../shacl2md/generator.py#L433)

Validate the SHACL graph against the SHACL specification.

#### Signature

```python
def validate(self):
    ...
```



## ShaclMarkdownGenerator

[Show source in generator.py:101](../../shacl2md/generator.py#L101)

#### Signature

```python
class ShaclMarkdownGenerator(Generator):
    def __init__(
        self,
        languages: List[str],
        output_dir: str = "./",
        shacl_shacl_validation: bool = False,
        version_directory: bool = False,
        crosslink_between_graphs: bool = False,
        jekyll_parent_page: str = "index",
        jekyll_layout: str = "default",
        jekyll_nav_order: int = 1,
        ontology_graphs: List[Union[str, Graph]] = None,
        logger: Logger = None,
    ):
        ...
```

#### See also

- [Generator](#generator)

### ShaclMarkdownGenerator().filter_graph

[Show source in generator.py:156](../../shacl2md/generator.py#L156)

Get all other graphs.

#### Arguments

- `graph_name` *str* - Name of the graph to filter.

#### Signature

```python
def filter_graph(self, graph_name: str):
    ...
```

### ShaclMarkdownGenerator().filter_language

[Show source in generator.py:147](../../shacl2md/generator.py#L147)

Get all other languages.

#### Arguments

- `lang` *str* - language to filter

#### Signature

```python
def filter_language(self, lang: str):
    ...
```

### ShaclMarkdownGenerator().generate

[Show source in generator.py:165](../../shacl2md/generator.py#L165)

Generate markdown documentation from SHACL files.

#### Arguments

- `exclude` - list of graph names for which docs should not be generated
- `**shacls` - Dictionary of SHACL files or Graphs to generate documentation for. The key is the name of the SHACL graph, the value is the filename of the SHACL file.

#### Raises

- `ValidationFailure` *pyshacl.errors.ValidationFailure* - Raised when the SHACL files do not validate against the SHACL specification.

#### Examples

```python
>>> from shacl2md import ShaclMarkdownGenerator
>>> sh_md = ShaclMarkdownGenerator(
...     ["nl", "en", "fr"],
...     "./output",
...     shacl_shacl_validation=True,
...     version_directory=True,
...     crosslink_between_graphs=True,
...     ontology_graphs=[
...         "/path_to_ontology/rdfs.ttl",
...     ]
... )
>>> sh_md.generate(
...     organizations="/path_to_shacl/organizations.shacl.ttl",
...     description="/path_to_shacl/description.shacl.ttl",
... )
```

#### Signature

```python
def generate(self, exclude: list = None, **shacls) -> None:
    ...
```



## ShaclSnippetGenerator

[Show source in generator.py:205](../../shacl2md/generator.py#L205)

#### Signature

```python
class ShaclSnippetGenerator(Generator):
    def __init__(
        self,
        languages: List[str] = ["en"],
        output_dir: str = "./",
        shacl_shacl_validation: bool = False,
        ontology_graphs: List[Union[str, Graph]] = None,
        logger: Logger = None,
    ):
        ...
```

#### See also

- [Generator](#generator)

### ShaclSnippetGenerator().generate

[Show source in generator.py:226](../../shacl2md/generator.py#L226)

Generate snippets from SHACL files. Place the snippets in the `.vscode` directory.

#### Arguments

- `**shacls` - Dictionary of SHACL files or Graphs to generate snippets for. The key is the name of the SHACL graph, the value is the filename of the SHACL file.

#### Raises

- `ValidationFailure` *pyshacl.errors.ValidationFailure* - Raised when the SHACL files do not validate against the SHACL specification.

#### Examples

```python
>>> from shacl2md import ShaclSnippetGenerator
>>> sh_snippet = ShaclSnippetGenerator()
>>> sh_snippet.generate(
...     organizations="/path_to_shacl/organizations.shacl.ttl",
...     description="/path_to_shacl/description.shacl.ttl",
... )
```

#### Signature

```python
def generate(self, **shacls):
    ...
```