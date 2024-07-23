struct fenwik_tree  
{  
    int n;  
    vector<int> fen;  
    fenwik_tree(int n)  
    {  
       fen = vector<int>(n + 1);  
       this->n = n;  
    }
    int sum(int p)  
    {  
       int s = 0;  
       while (p >= 1)s += fen[p], p -= p & -p;  
       return s;  
    }  
    int sum(int l, int r)  
    {  
       return sum(r) - (l > 1 ? sum(l - 1) : 0);  
    }  
    void add(int p, int x)  
    {  
       while (p <= n)fen[p] += x, p += p & -p;  
    }  
};