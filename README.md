# kuskal

package kruskal;
import java.util.*;
import java.lang.*;
import java.io.*;
public class Kruskal {
    int V,E;
    class Edge implements Comparable<Edge>
    {   
        int src, dest, weight;
        public int compareTo(Edge compareEdge)
        {
            return this.weight - compareEdge.weight;
        }
    }
    Edge edge[];
    int leader[];
    Kruskal(int v, int e){
        V = v;
        E = e;
        edge = new Edge[E];
        leader=new int [V];
        
        for(int i=0; i<E; i++){
            edge[i] = new Edge();
        }
    }
    
    void Union(int srcV, int destV){
        int newleader;
        if(srcV<destV){
            newleader=srcV;
            for(int i=0;i<V;i++){
                if(leader[i]==destV){
                    leader[i]=newleader;
                }
            }
        }
        else{
            newleader=destV;
            for(int i=0;i<V; i++){
                if(leader[i]==srcV){
                    leader[i]=newleader;
                }
            }
        }
    }
    
    int Find(int value){
        return leader[value];
    }
    
    void KruskalMST(){
        Edge result[]=new Edge[V-1];
        int i=0;
        for(i=0; i<result.length; i++){
            result[i]=new Edge();
        }
        Arrays.sort(edge);
        
        for(i=0; i<V;++i){
            leader[i]=i;
        }
        i=0;
        for(int e=0; e<edge.length; e++){
            Edge next_edge=edge[e];
            int x=Find(next_edge.src);
            int y=Find(next_edge.dest);
            if(x!=y){
                result[i++]=next_edge;
                Union(x,y);
            }
        }
        int minimumcost=0;
        for(i=0; i<result.length; i++){
            System.out.println(result[i].src+" -- "+result[i].dest+" ==> "+ result[i].weight);
            minimumcost+=result[i].weight;
        }
        System.out.println("Minimum Cost Spanning Tree " + minimumcost);
    }
    public static void main(String[] args) {
        Scanner Input= new Scanner(System.in);
        int vertex_num, edge_num,i;
        System.out.println("Enter vertex number: ");
        vertex_num=Input.nextInt();
        System.out.println("Enter Edge number: ");
        edge_num=Input.nextInt();
        Kruskal graph = new Kruskal(vertex_num, edge_num);
        for(i=0; i<edge_num; i++){
            System.out.println("Enter source number for "+(i+1)+":");
            graph.edge[i].src = Input.nextInt();
            System.out.println("Enter destination number for "+(i+1)+":");
            graph.edge[i].dest = Input.nextInt();
            System.out.println("Enter weight number for "+(i+1)+":");
            graph.edge[i].weight = Input.nextInt();
        }
        graph.KruskalMST();
    }
}
