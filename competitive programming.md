# competitive programming

### input: 

```java
static class FastReader {
    BufferedReader br;
    StringTokenizer st;

    public FastReader() {
        br = new BufferedReader(new InputStreamReader(System.in));
    }

    String next() {
        while(st == null || !st.hasMoreElements()) {
            try {
                st = new StringTokenizer(br.readLine());
            }
            catch(IOException e) {
                e.printStackTrace();
            }
        }
        return st.nextToken();
    }

    int nextInt() {
        return Integer.parseInt(next());
    }
}
```

### output:

```java
BufferedWriter output = new BufferedWriter(new OutputStreamWriter(System.out));
for (int i: subordinates) output.write(i + " ");
```

