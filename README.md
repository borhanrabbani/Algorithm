Prim's Algorithm:

#include <stdio.h>
#define inf 10000
#define NIL -1


int key[21], adj[21][21], E, ver, p[21], extract[21];

void input()
{
    int i,u,v,w;
    scanf("%d %d", &E, &ver);
    for(i=0; i<E; i++)
    {
        scanf("%d %d %d", &u,&v,&w);
        adj[u][v]=w;
        adj[v][u]=w;

    }
}

int minimum()
{
    int i, min=inf, min_pos;
    for(i=1; i<=ver; i++)
    {
        if(extract[i]==0)
        {
            if(key[i]< min)
            {
                min=key[i];
                min_pos = i;
            }
        }
    }

    extract[min_pos] = -1;
    return min_pos;
}

void output(int root)
{
    int i, sum=0;
    for(i=1; i<=ver; i++)
    {
        if(i!=root)sum=sum+adj[i][p[i]];
    }
    printf("Results: %d\n", sum);
}

void prims(int root)
{
    int i, c, u, v;
    for(i=1; i<=ver; i++)
    {
        key[i]=inf;
        p[i]=NIL;
        extract[i]=0;
    }
    key[root] = 0;
    c=ver;
    while(c)
    {
        u= minimum();
        c--;
        for(v=1; v<=ver; v++)
        {
            if(adj[u][v] !=0)
            {
                if(extract[v] == 0 && adj[u][v]< key[v])
                {
                    p[v]=u;
                    key[v]=adj[u][v];
                }
            }
        }
    }
}

int main()
{
    freopen("in.txt", "r", stdin);
    input();

    prims(5);

    output(5);
    return 0;
}
