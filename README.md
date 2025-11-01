#include <iostream>
#include <string>
#include <map>
#include <vector>
#include <algorithm>
using namespace std;

class Chatbot {
    map<string, string> responses;
    vector<string> memory;
public:
    Chatbot() {
        responses["hello"] = "Hey there! How can I help you today?";
        responses["how are you"] = "I'm just code, but I'm feeling efficient!";
        responses["bye"] = "Goodbye! Come back soon!";
        responses["help"] = "You can ask me about time, date, or basic questions.";
    }

    string processInput(string input) {
        transform(input.begin(), input.end(), input.begin(), ::tolower);
        memory.push_back(input);
        for (auto& [key, value] : responses) {
            if (input.find(key) != string::npos) return value;
        }
        return "Hmm... I'm not sure about that. Can you rephrase?";
    }

    void showMemory() {
        cout << "Chat history: \n";
        for (auto& msg : memory) cout << "- " << msg << endl;
    }
};

int main() {
    Chatbot bot;
    cout << "AI Chatbot started. Type 'exit' to quit.\n";
    string input;
    while (true) {
        cout << "You: ";
        getline(cin, input);
        if (input == "exit") break;
        cout << "Bot: " << bot.processInput(input) << "\n";
    }
    bot.showMemory();
    return 0;
}
