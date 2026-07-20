```c#
using System;
using System.Collections.Generic;
using System.Linq;

public class MySimpleHashTable
{
    private readonly int _size;
    private readonly List<Entry>[] _buckets;

    public MySimpleHashTable(int size)
    {
        _size = size;
        _buckets = new List<Entry>[size];
        
        // Initialize each bucket as an empty list
        for (int i = 0; i < size; i++)
        {
            _buckets[i] = new List<Entry>();
        }
    }

    // The "Magic" Hash Function
    private int GetHash(string key)
    {
        // Get the absolute value of the built-in C# hash code
        // and use Modulo (%) to keep it within our array bounds
        return Math.Abs(key.GetHashCode()) % _size;
    }

    public void Add(string key, string value)
    {
        int index = GetHash(key);
        var bucket = _buckets[index];

        // Check if key already exists to update it
        var existing = bucket.FirstOrDefault(e => e.Key == key);
        if (existing != null)
        {
            existing.Value = value;
        }
        else
        {
            bucket.Add(new Entry { Key = key, Value = value });
        }
    }

    public string Get(string key)
    {
        int index = GetHash(key);
        var bucket = _buckets[index];

        // Search the small list in that bucket
        var entry = bucket.FirstOrDefault(e => e.Key == key);
        return entry?.Value; // Returns null if not found
    }
}
```