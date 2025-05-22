using System.Collections.Generic;

public class Node
{
    public string Title { get; set; }
    public List<Node> Children { get; set; } = new List<Node>();

    public Node(string title)
    {
        Title = title;
    }

    public void AddChild(Node child)
    {
        if (Children.Count < 3)
            Children.Add(child);
        else
            Console.WriteLine("Un nœud peut avoir au maximum 3 enfants.");
    }
}


public class MindMap
{
    public Node Root { get; set; }

    public MindMap(string rootTitle)
    {
        Root = new Node(rootTitle);
    }

    public void AddNode(string parentTitle, string childTitle)
    {
        var parentNode = FindNode(Root, parentTitle);
        if (parentNode != null)
        {
            var childNode = new Node(childTitle);
            parentNode.AddChild(childNode);
        }
        else
        {
            Console.WriteLine("Nœud parent non trouvé.");
        }
    }

    private Node FindNode(Node currentNode, string title)
    {
        if (currentNode.Title == title)
            return currentNode;

        foreach (var child in currentNode.Children)
        {
            var result = FindNode(child, title);
            if (result != null)
                return result;
        }

        return null;
    }

    public void ListNodes(Node currentNode, string indent = "")
    {
        Console.WriteLine($"{indent}- {currentNode.Title}");
        foreach (var child in currentNode.Children)
        {
            ListNodes(child, indent + "  ");
        }
    }
}


   class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Bienvenue dans l'application MindMap CLI!");

        var mindMap = new MindMap("Idées Principales");

        while (true)
        {
            Console.WriteLine("\nChoisissez une option:");
            Console.WriteLine("1. Ajouter un nœud");
            Console.WriteLine("2. Lister la carte");
            Console.WriteLine("3. Quitter");
            var choice = Console.ReadLine();

            switch (choice)
            {
                case "1":
                    Console.Write("Titre du nœud parent : ");
                    var parentTitle = Console.ReadLine();
                    Console.Write("Titre du nouveau nœud : ");
                    var childTitle = Console.ReadLine();
                    mindMap.AddNode(parentTitle, childTitle);
                    break;
                case "2":
                    mindMap.ListNodes(mindMap.Root);
                    break;
                case "3":
                    return;
                default:
                    Console.WriteLine("Option invalide.");
                    break;
            }
        }
    }
}
    
