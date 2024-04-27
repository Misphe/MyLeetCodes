#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

class Solution {
public:
    int calculateDistance(string &ring, int index1, int index2) {
        int length = ring.length();
        int rawDistance = abs(index1 - index2);
        int circularDistance = length - rawDistance;
        return min(rawDistance, circularDistance);
    }

    int findMinWay(string &ring, string &key, unordered_map<char, vector<int>> &positions, int currentSearchedIndex, int currentlyAt, int length, vector<vector<int>> &memo)
    {
        if (currentSearchedIndex == key.length()) {
            return length;
        }
        if (memo[currentSearchedIndex][currentlyAt] != -1) {
            return length + memo[currentSearchedIndex][currentlyAt];
        }
        char searchedChar = key[currentSearchedIndex];
        vector<int> &searchedCharPositions = positions[searchedChar];
        int minDistance = 9999;
        for (int searchedCharPosition : searchedCharPositions) {
            int distance = calculateDistance(ring, searchedCharPosition, currentlyAt);
            int candidateDistance = findMinWay(ring, key, positions, currentSearchedIndex + 1, searchedCharPosition, length + distance, memo);
            if (candidateDistance < minDistance) {
                minDistance = candidateDistance;
            }
        }
        if (minDistance != 9999) {
            memo[currentSearchedIndex][currentlyAt] = minDistance - length;
        }
        return minDistance;
    }

    int findRotateSteps(string ring, string key) {

        unordered_map<char, vector<int>> positions;
        for (int i = 0; i < ring.length(); i++) {
            positions[ring[i]].push_back(i);
        }
        vector<vector<int>> memo(key.length(), vector<int>(ring.length(), -1));
        return findMinWay(ring, key, positions, 0, 0, 0, memo) + key.length();
    }
};
