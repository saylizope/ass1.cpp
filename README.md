# ass1.cpp
BS and DFS

#include<stdio.h>
#define MAX 20
#include<iostream>
using namespace std;

int adj[ MAX ][ MAX ];
bool visited[ MAX ];
int n; /* Denotes number of nodes in the graph */

class graph
{
public:
void create_graph();
void display();
void dfs( int v );
void bfs( int v );
};

void graph::create_graph()
{
    int i, maxedges, origin, destin,pp;

    cout<<"Enter number of nodes : ";
    cin>>n;
    pp=n-1;
    maxedges = n*pp;

    for ( i = 1;i <= maxedges;i++ )
        {
            cout<<"Enter edge %d( 0 0 to quit ) : "<<i ;
            cin>>origin; cin>>destin;


            if ( ( origin == 0 ) && ( destin == 0 ) )
                break;

            if ( origin > n || destin > n || origin <= 0 || destin <= 0 )
                {
                    cout<<"Invalid edge!\n";
                    i=i-1;
                }
            else
                {
                    adj[ origin ][ destin ] = 1;
                }
        } /*End of for*/
} /*End of create_graph()*/

void graph::display()
{
    int i, j;

    for ( i = 1;i <= n;i++ )
        {
            for ( j = 1;j <= n;j++ )
                cout<< "%4d"<<adj[ i ][ j ];

            cout<<"\n";
        }
} /*End of display()*/


void graph::dfs( int v )
{
    int i, stack[ MAX ], top = -1, pop_v;

    top++;
    stack[ top ] = v;

    while ( top >= 0 )
        {
            pop_v = stack[ top ];
            top=top-1; /*pop from stack*/

            if ( visited[ pop_v ] == false )
                {
                    cout<<pop_v;
                    visited[ pop_v ] = true;
                }
            else
                continue;

            for ( i = n;i >= 1;i-- )
                {
                    if ( adj[ pop_v ][ i ] == 1 && visited[ i ] == false )
                        {
                            top++; /* push all unvisited neighbours of pop_v */
                            stack[ top ] = i;
                        } /*End of if*/
                } /*End of for*/
        } /*End of while*/
} /*End of dfs()*/

void graph::bfs( int v )
{
    int i, front, rear;
    int que[ 20 ];
    front = rear = -1;

    cout<<v;
    visited[ v ] = true;
    rear++;
    front++;
    que[ rear ] = v;

    while ( front <= rear )
        {
            v = que[ front ]; /* delete from queue */
            front++;

            for ( i = 1;i <= n;i++ )
                {
                    /* Check for adjacent unvisited nodes */

                    if ( adj[ v ][ i ] == 1 && visited[ i ] == false )
                        {
                            cout<<i;
                            visited[ i ] = true;
                            rear++;
                            que[ rear ] = i;
                        }
                }
        } /*End of while*/
} /*End of bfs()*/


int main()
{
    int i, v, choice;
    graph g;
    g.create_graph();

    while ( 1 )
        {
            cout<<"\n";
            cout<<"1. Adjacency matrix\n";
            cout<<"2. Depth First Search\n";
            cout<<"3. Breadth First Search\n";
            cout<<"Enter your choice : ";
            cin>>choice;

            switch ( choice )
                {

                case 1:
                    cout<<"Adjacency Matrix\n";
                    g.display();
                    break;

                case 2:
                    cout<<"Enter starting node for Depth First Search : ";
                    cin>>v;

                    for ( i = 1;i <= n;i++ )
                        visited[ i ] = false;

                    g.dfs( v );

                    break;



                case 3:
                    cout<<"Enter starting node for Breadth First Search : ";

                    cin>>v;

                    for ( i = 1;i <= n;i++ )
                        visited[ i ] = false;

                    g.bfs( v );

                    break;



                default:
                    cout<<"Wrong choice\n";

                    break;
                } /*End of switch*/
        } /*End of while*/
return 0;
} /*End of main()*/
