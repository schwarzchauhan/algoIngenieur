# __Count Sort__  

***k*** is the maximum value element  in array a
> It assumes that each element in the array is in range `[0,k]`

### ___basic idea___  
to determine, for each input element X, the number of elements less than
X. 
This information can be used to place it directly into its correct position

### ___arrays data structure used___
`ct[i]` is the occurrence of number i in the array  
`cum[i]` is the cumulative sum till occ[i](including occ[i]);

`0 based indexing assumed in array a & sorted array s`


    #include<bits/stdc++.h>
    using namespace std;
    #define ll long long int
    #define co cout<<

    void countSort(ll a[], ll n)   // O(k + n)
    {
        ll k = INT_MIN;
        for (ll i = 0; i < n; i++){      // to find k  , O(n)
            k = max(a[i], k);
        }

        ll ct[k+1];
        ll cum[k+1];
        for (ll i = 0; i <= k; i++){       // O(k), k can be greater than n
            ct[i] = 0;
            cum[i] = 0;
        }


        for (ll i = 0; i < n; i++){    //  O(n)
            ct[a[i]]++;
        }

        cum[0] = ct[0];
        for (ll i = 1; i <= k; i++){     // O(k), k can be greater than n
            cum[i] = cum[i-1] + ct[i];
        }

        ll s[n];
        for (ll i = 0; i < n; i++)      //  O(n)
        {
            ll index = cum[a[i]]-1;
            s[index] = a[i];

            cum[a[i]]--;
        }

        for (ll i = 0; i < n; i++)     //  O(n)
        {
            co s[i]<<" ";
        }co endl;
    }

    int main(){

        #ifndef ONLINE_JUDGE
            freopen("input.txt", "r", stdin);
            freopen("output.txt", "w", stdout);
        #endif

        ll T;
        cin>>T;
        for (ll tc = 0; tc < T; tc++){
            
            ll n;
            cin>>n;
            ll a[n];

            for (ll i = 0; i < n; i++)
            {
                cin>>a[i];
            }
            countSort(a,n);


            
        }

        return 0;
    }

    /*

        Sample input 
        1
        5
        89 9 0 5 3

        Sample output 
        0 3 5 9 89 

    */

> It is good algorithm in case k = O(n)

`