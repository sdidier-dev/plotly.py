---
jupyter:
  jupytext:
    notebook_metadata_filter: all
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.13.7
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.9.0
  plotly:
    description: How to use selections in Python. Examples of adding and styling selections.
    display_as: file_settings
    language: python
    layout: base
    name: Selections
    order: 26
    permalink: python/selections/
    thumbnail: thumbnail/make_selection.jpg
---

## Adding Selections

*New in 5.10*

You can add persistent selections to a rendered figure using the **Box Select** and **Lasso Select** tools in the mode bar.
To add multiple selections, select **Shift** when making new selections.
To clear a selection, double-click it. On a subplot you can clear all selections by double-clicking any unselected area of the subplot.



You can also add selections to a figure that displays when it renders using `fig.add_selection`.
Here, we add a rectangular selection with a region between `3.0` and `6.5` on the x axis and between `3.5` and `5.5` on the y axis.


```python
import plotly.express as px

df = px.data.iris()

fig = px.scatter(df, x="sepal_width", y="sepal_length")
fig.add_selection(type="rect", x0=3.0, y0=6.5, x1=3.5, y1=5.5)

fig.show()
```

## Styling Selections


In the above example, we added a selection to the figure that is displayed when the figure renders.
`fig.add_selection` accepts additional properties that you can use to style the selection. Here, we add a `color`, `width`, and specify the `dash` type for the selection.


```python
import plotly.express as px

df = px.data.iris()

fig = px.scatter(df, x="sepal_width", y="sepal_length")
fig.add_selection(type="rect",
    x0=2.5, y0=6.5, x1=3.5, y1=5.5,
    line=dict(
        color="Crimson",
        width=2,
        dash="dash",
    ))

fig.show()

```

## Fill Color for Active Selections

You can style active selections with `activeselection`. In this example, we set active selections to appear with a `fillcolor` of `blue`.

```python
import plotly.express as px

df = px.data.iris()

fig = px.scatter(df, x="sepal_width", y="sepal_length")
fig.add_selection(type="rect", x0=3.0, y0=6.5, x1=3.5, y1=5.5)

fig.update_layout(dragmode='select',
                  activeselection=dict(fillcolor='blue'))

fig.show()
```

## Styling New Selections

You can style new selections made on the figure by setting properties on `newselection`.
Try making a new selection on the figure to try it out.

```python
import plotly.express as px

df = px.data.iris()

fig = px.scatter(df, x="sepal_width", y="sepal_length")

fig.update_layout(dragmode='select',
                  newselection=dict(line=dict(color='blue')))

fig.show()
```

## More on Selections

For more on selections, see the [selections section of the `dcc.Graph` page](https://dash.plotly.com/dash-core-components/graph#selections) in the Dash docs.