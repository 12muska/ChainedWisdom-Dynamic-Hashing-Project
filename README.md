# ChainedWisdom-Dynamic-Hashing-Project

This project involves the implementation of an advanced data structure - a generic hash table with chaining - using C++. The hash table is designed to handle different types of keys and values, demonstrating proficiency in data structures and algorithms.

Code Explanation:
Let's go through the code step by step:

1. HashNode Structure:
cpp
Copy code
template <typename K, typename V>
struct HashNode {
    K key;
    V value;

    HashNode(const K& k, const V& v) : key(k), value(v) {}
};
HashNode represents a node in the hash table, storing a key-value pair.
It's a template structure, allowing flexibility for different key and value types.
The constructor initializes the key and value.
2. HashMap Class:
cpp
Copy code
template <typename K, typename V>
class HashMap {
private:
    std::vector<std::list<HashNode<K, V>>> table;
    size_t capacity;

    size_t hashFunction(const K& key) const {
        std::hash<K> hasher;
        return hasher(key) % capacity;
    }

public:
    HashMap(size_t cap) : capacity(cap), table(cap) {}

    void insert(const K& key, const V& value) {
        size_t index = hashFunction(key);
        table[index].emplace_back(key, value);
    }

    bool search(const K& key, V& value) const {
        size_t index = hashFunction(key);

        for (const auto& node : table[index]) {
            if (node.key == key) {
                value = node.value;
                return true;
            }
        }

        return false;
    }

    void display() const {
        for (size_t i = 0; i < capacity; ++i) {
            std::cout << "Bucket " << i << ": ";
            for (const auto& node : table[i]) {
                std::cout << "(" << node.key << ", " << node.value << ") ";
            }
            std::cout << std::endl;
        }
    }
};
HashMap is a template class representing the hash table.
It uses a vector of lists (std::vector<std::list<HashNode<K, V>>>) for chaining.
The hashFunction calculates the index in the table based on the key's hash value.
The constructor initializes the capacity and creates an empty table.
insert adds a key-value pair to the hash table, handling collisions with chaining.
search looks for a value based on a key.
display prints the contents of the hash table.
3. Main Function:
cpp
Copy code
int main() {
    HashMap<std::string, int> hashMap(10);

    hashMap.insert("John", 28);
    hashMap.insert("Jane", 22);
    hashMap.insert("Doe", 35);

    std::cout << "Hash Table Contents:" << std::endl;
    hashMap.display();

    int age;
    if (hashMap.search("Jane", age)) {
        std::cout << "Age of Jane: " << age << std::endl;
    } else {
        std::cout << "Jane not found in the hash table." << std::endl;
    }

    return 0;
}
In the main function, an instance of HashMap is created with a capacity of 10.
Key-value pairs ("John", 28), ("Jane", 22), and ("Doe", 35) are inserted into the hash table.
The contents of the hash table are displayed using the display method.
A search for the age of "Jane" is performed, and the result is printed.
