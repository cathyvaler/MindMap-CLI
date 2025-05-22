public class Node
{
    public string Title { get; set; }
    public List<Node> Children { get; set; } = new List<Node>();
    
    public Node(string title)
    {
        Title = title;
    }
}

// MindMap.cs
public class MindMap
{
    public Node Root { get; set; }
    public string Name { get; set; }
    
    public MindMap(string name, string rootTitle)
    {
        Name = name;
        Root = new Node(rootTitle);
    }
}# MindMap-CLI
