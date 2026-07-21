A record in C# (introduced in C# 9) is a lightweight class designed purely for holding data. Declaring:


```cs
private record TabEntry(string AbsoluteUrl, string Title);
```
is shorthand for this class:


```cs

private class TabEntry{    public string AbsoluteUrl { get; init; }    public string Title { get; init; }    public TabEntry(string absoluteUrl, string title)    {        AbsoluteUrl = absoluteUrl;        Title = title;    }}
```



The compiler auto-generates the constructor, the properties, equality comparison, and ToString() for you.

Do we actually need it here?

No — it's just a convenience. The only thing using TabEntry is _visibleTabs, which is a list used to render the dropdown. A simple tuple (string AbsoluteUrl, string Title) would work equally well and requires zero extra declaration:

```cs

private List<(string AbsoluteUrl, string Title)> _visibleTabs = [];
```

The record was added to keep the razor template readable (tab.AbsoluteUrl, tab.Title) rather than tab.Item1, tab.Item2 — but named tuples achieve the same thing. It's a style preference, not a necessity. Want me to replace it with a named tuple to remove the extra declaration?