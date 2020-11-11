# individual_Coursework  

#include <iostream>
#include <fstream>
#include <vector>
#include<bits/stdc++.h>

using namespace std;
//tASK1

vector<string> getWords(string file, int startline, int endline) { 
    /*
    Gets all words form a text file between specified lines

    Parameters:
    string file: path to the text file

    Output:
    a vector<string> with words all free from punctuation
    */

    // Get number of lines
    fstream textFile;
    textFile.open(file);

    int num_of_lines;
    string mockup_line;
    while (getline(textFile, mockup_line)) {
        num_of_lines++;
    }

    textFile.close();

    // Check inputs are valid
    if (endline < startline) {
        throw runtime_error("End line must not be before the start line");
    }

    if (startline > num_of_lines || endline > num_of_lines) {
        throw runtime_error("Start line or end line fall out of the file's size");
    }
     
    if (startline < 0 || endline < 0) {
        throw runtime_error("Line numbers must not be negative");
    }

    // Get file's lines in a vector from startline to endline
    textFile.open(file);    

    string line;
    vector<string> lines;

    for (int i = 0; i < endline; i++) {
        getline(textFile, line);
        if (i < startline - 1) continue;
        lines.push_back(line);
    }

    textFile.close();

    // Get all words in a vector, even repeated ones
    vector<string> words;

    // Go through all lines and get words separatedly in a vector of strings
    for (int i = 0; i < lines.size(); i++) {
        string word;
        stringstream strm(lines[i]);
        while (strm >> word) {
            // Remove punctuation from word
            for (int j = 0, length = word.length(); j < length; j++) {
                if (ispunct(word[j])) {
                    word.erase(j--, 1);
                    length = word.size();
                }
            }
            // Add word to deposit
            words.push_back(word);
        }
    }

    // Debug
    for (int i = 0; i < words.size(); i++) {cout << words[i] << endl;}

    return words;
}
//tASK2
class Bst {
    public:
        Node * root;

        Node * insert(Node * node, int key) {
            if(node == NULL) {
                node = new Node;
                node->Key = key;
                node->Left = NULL;
                node->Right = NULL;
                node->Parent = NULL;
            } else if (node->Key < key) {
                node->Right = insert(node->Right, key);
                node->Right->Parent = node;
            } else {
                node->Left = insert(node->Left, key);
                node->Left->Parent = node;
            }

            return node;
        }

        void * insert(int key) {
            root = insert(root, key);
        }
    
        // Searches for the specified word
        // Returns number of time it appears on the BST
        int search(int key) {

        }
};

class Node {
    public:
        int Key;
        Node * Left;
        Node * Right;
        Node * Parent;
};

int main() {

    // Get all sonet's words in a vector
    vector<string> words;
    words = getWords("shakespeare.txt", 253, 2867);

    // Build a binary search tree with those words
    Bst bst = Bst();    

    return 0;
}
