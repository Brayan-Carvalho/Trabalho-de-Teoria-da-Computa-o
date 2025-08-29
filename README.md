    #include <iostream>
    #include <set>
    #include <vector>
    #include <algorithm>
    #include <locale.h>
    using namespace std;
    
    // Função para imprimir conjuntos
    void printSet(const set<char>& s, string name) {
        cout << name << " = { ";
        for (auto it = s.begin(); it != s.end(); ++it) {
            cout << *it;
            if (next(it) != s.end()) cout << ", ";
        }
        cout << " }" << endl;
    }
    
    // União
    set<char> setUnion(const set<char>& A, const set<char>& B) {
        set<char> result;
        set_union(A.begin(), A.end(), B.begin(), B.end(),
                  inserter(result, result.begin()));
        return result;
    }
    
    // Interseção
    set<char> setIntersection(const set<char>& A, const set<char>& B) {
        set<char> result;
        set_intersection(A.begin(), A.end(), B.begin(), B.end(),
                         inserter(result, result.begin()));
        return result;
    }
    
    // Diferença A - B
    set<char> setDifference(const set<char>& A, const set<char>& B) {
        set<char> result;
        set_difference(A.begin(), A.end(), B.begin(), B.end(),
                       inserter(result, result.begin()));
        return result;
    }
    
    // Verificação de igualdade
    bool areEqual(const set<char>& A, const set<char>& B) {
        return A == B;
    }
    
    // Subconjunto
    bool isSubset(const set<char>& A, const set<char>& B) {
        return includes(B.begin(), B.end(), A.begin(), A.end());
    }
    
    // Produto cartesiano
    vector<pair<char,char>> cartesianProduct(const set<char>& A, const set<char>& B) {
        vector<pair<char,char>> result;
        for (char a : A) {
            for (char b : B) {
                result.push_back({a, b});
            }
        }
        return result;
    }
    
    // Imprimir produto cartesiano
    void printCartesian(const vector<pair<char,char>>& prod, string name) {
        cout << name << " = { ";
        for (size_t i = 0; i < prod.size(); i++) {
            cout << "(" << prod[i].first << "," << prod[i].second << ")";
            if (i != prod.size()-1) cout << ", ";
        }
        cout << " }" << endl;
    }
    
    // Relação binária como subconjunto do produto cartesiano
    bool belongsToRelation(const vector<pair<char,char>>& relation, pair<char,char> element) {
        return find(relation.begin(), relation.end(), element) != relation.end();
    }
    
    int main() {
        setlocale(LC_ALL,"portuguese_Brazil");
        
        int opcao;
        do {
            set<char> A, B;
            int n, m;
            char val;
    
            cout << "Digite o numero de elementos do conjunto A: ";
            cin >> n;
            cout << "Digite os elementos de A:\n";
            for (int i = 0; i < n; i++) {
                cin >> val;
                A.insert(val);
            }
    
            cout << "Digite o numero de elementos do conjunto B: ";
            cin >> m;
            cout << "Digite os elementos de B:\n";
            for (int i = 0; i < m; i++) {
                cin >> val;
                B.insert(val);
            }
    
            printSet(A, "A");
            printSet(B, "B");
    
            // Operações básicas
            printSet(setUnion(A,B), "A U B");
            printSet(setIntersection(A,B), "A ^ B");
            printSet(setDifference(A,B), "A - B");
    
            cout << "A == B ? " << (areEqual(A,B) ? "Sim" : "Nao") << endl;
            cout << "A sub B ? " << (isSubset(A,B) ? "Sim" : "Nao") << endl;
            cout << "A != B ? " << (!areEqual(A,B) ? "Sim" : "Nao") << endl;
    
            // Produto cartesiano
            auto prod = cartesianProduct(A,B);
            printCartesian(prod, "A × B");
    
            // Relação exemplo: {(a,b), (b,c)}
            vector<pair<char,char>> R = { {'a','b'}, {'b','c'} };
            cout << "R = { (a,b), (b,c) }" << endl;
            cout << "(a,b) pertence a R? "
                 << (belongsToRelation(R, {'a','b'}) ? "Sim" : "Nao") << endl;
            cout << "(c,a) pertence a R? "
                 << (belongsToRelation(R, {'c','a'}) ? "Sim" : "Nao") << endl;
    
            cout << "\nDeseja continuar? (1 - Sim / 2 - Nao): ";
            cin >> opcao;
            cout << endl;
    
        } while(opcao == 1);
    
       return 0;
    }

