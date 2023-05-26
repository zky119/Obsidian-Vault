
```python
from matplotlib.colors import ListedColormap
from sklearn.inspection import DecisionBoundaryDisplay

def plot_decision_boundary(model, X, y):
    color = ["r", "g", "b"]
    marker = ["o", "v", "x"]
    class_label = np.unique(y)
    cmap = ListedColormap(color[: len(class_label)])
    DecisionBoundaryDisplay.from_estimator(
        model,
        X,
        response_method="predict",
        alpha=0.5,
        # cmap=cmap,
        grid_resolution=100,
        ax=plt.gca()
        )

    for i, class_ in enumerate(class_label):
        plt.scatter(
            x=X[y == class_, 0],
            y=X[y == class_, 1],
            c=cmap.colors[i],
            label=class_,
            marker=marker[i],
            s=15
            )
    plt.legend()
```

![[Pasted image 20230525144458.png]]