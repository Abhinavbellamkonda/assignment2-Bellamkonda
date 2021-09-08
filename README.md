# assignment2-Bellamkonda
The second Assignment.

# Abhinav Bellamkonda 
###### my favorite place is taj mahal.

An immense mausoleum of white marble, built in Agra between 1631 and 1648 by order of the **Mughal emperor** Shah Jahan in memory of his favourite wife, the **Taj Mahal** is the jewel of Muslim art in India and one of the universally admired masterpieces of the **world's heritage**.

---

### Directions for travelling from Maryville to Taj Mahal

1. Firstly we need to catchup a flight from maryville to India.
2. The nearby airport is kansas, so we need to place the destination as delhi.
3. After reaching to Delhi. There are several ways to reach Agra.
    1. we can go by train to agra
    2. we can book a cab.
    3. we can book a bus.
    4. we can take a rental car.
4. This way we can reach to Taj Mahal.

### Items that are required for the trip
* Proper accomodation is required in Delhi
* Personal vehicle is suggested to cover all the places.
* Enough liquid cash must be carried.

Link of my personal Info [AboutMe](https://github.com/Abhinavbellamkonda/assignment2-Bellamkonda/blob/main/AboutMe.md)

---

## List of food/drinks I wish you will enjoy if you try
In the table i will describe the food items location and price of the item

| Food | Place | cost |
| ---| ---| ---: |
| Keema Biryani | Hyderabad | 450Rs/- |
| Manchuria | Ameerpet | 30Rs/- |
| Chicken Kurma | Patha Basti | 300/- |
| Haleem | Old City | 250/- |

---

## Pithy Quotes

> “I saw that you were perfect, and so I loved you. Then I saw that you were not perfect and I loved you even more.” <br> — *Angelita Lim*

> “I love you for all that you are, all that you have been and all that you will be.” <br> — *Abhinav Bellamkonda*

---

## Code Fencing

> Discription: The modification is extremely simple: In the previous article we chosen a vertex with excess without any particular rule. But it turns out, that if we always choose the vertices with the greatest height, and apply push and relabel operations on them, then the complexity will become better. Moreover, to select the vertices with the greatest height we actually don't need any data structures, we simply store the vertices with the greatest height in a list, and recalculate the list once all of them are processed (then vertices with already lower height will be added to the list), or whenever a new vertex with excess and a greater height appears (after relabeling a vertex).<br> <br>

Despite the simplicity, this modification reduces the complexity by a lot. To be precise, the complexity of the resulting algorithm is O(VE+V2E−−√), which in the worst case is O(V3).<br><br>

This modification was proposed by Cheriyan and Maheshwari in 1989.

Here is the link: <br>
<https://cp-algorithms.com/graph/push-relabel-faster.html>

Here is code for `Flow Graph`: 

```
const int inf = 1000000000;

int n;
vector<vector<int>> capacity, flow;
vector<int> height, excess;

void push(int u, int v)
{
    int d = min(excess[u], capacity[u][v] - flow[u][v]);
    flow[u][v] += d;
    flow[v][u] -= d;
    excess[u] -= d;
    excess[v] += d;
}

void relabel(int u)
{
    int d = inf;
    for (int i = 0; i < n; i++) {
        if (capacity[u][i] - flow[u][i] > 0)
            d = min(d, height[i]);
    }
    if (d < inf)
        height[u] = d + 1;
}

vector<int> find_max_height_vertices(int s, int t) {
    vector<int> max_height;
    for (int i = 0; i < n; i++) {
        if (i != s && i != t && excess[i] > 0) {
            if (!max_height.empty() && height[i] > height[max_height[0]])
                max_height.clear();
            if (max_height.empty() || height[i] == height[max_height[0]])
                max_height.push_back(i);
        }
    }
    return max_height;
}

int max_flow(int s, int t)
{
    height.assign(n, 0);
    height[s] = n;
    flow.assign(n, vector<int>(n, 0));
    excess.assign(n, 0);
    excess[s] = inf;
    for (int i = 0; i < n; i++) {
        if (i != s)
            push(s, i);
    }

    vector<int> current;
    while (!(current = find_max_height_vertices(s, t)).empty()) {
        for (int i : current) {
            bool pushed = false;
            for (int j = 0; j < n && excess[i]; j++) {
                if (capacity[i][j] - flow[i][j] > 0 && height[i] == height[j] + 1) {
                    push(i, j);
                    pushed = true;
                }
            }
            if (!pushed) {
                relabel(i);
                break;
            }
        }
    }

    int max_flow = 0;
    for (int i = 0; i < n; i++)
        max_flow += flow[i][t];
    return max_flow;
}

```

Here is the link: <br>
<https://cp-algorithms.com/graph/push-relabel-faster.html>
