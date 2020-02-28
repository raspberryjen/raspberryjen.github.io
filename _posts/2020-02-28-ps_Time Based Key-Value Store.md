---
title: 
categories: leetcode
tags:
- HashTable
- TreeMap

---


** TreeMap **
TreeMap is sorted with key's default comparator

[https://www.geeksforgeeks.org/treemap-in-java/](https://www.geeksforgeeks.org/treemap-in-java/){:target="_blank"}


[https://leetcode.com/submissions/detail/307547505/](https://leetcode.com/submissions/detail/307547505/){:target="_blank"}
```java
class TimeMap {
    Map<String, TreeMap<Integer,String>> datamap;

    /** Initialize your data structure here. */
    public TimeMap() {
        datamap=new HashMap<>();
            
    }
    
    public void set(String key, String value, int timestamp) {
        TreeMap<Integer,String> map=datamap.getOrDefault(key,new TreeMap<Integer,String>());
        map.put(timestamp,value);
        datamap.put(key, map);
        // System.out.println(datamap);
    }
    
    public String get(String key, int timestamp) {
        TreeMap<Integer,String> map=datamap.getOrDefault(key, new TreeMap<Integer,String>());
        Integer ts=map.floorKey(timestamp);
        return ts!=null ? map.get(ts):"";
    }
}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
 ```

my soltuion : time limit

[](){:target="_blank"}

```java
class TimeMap {
    Map<String, Map<Integer,String>> datamap;

    /** Initialize your data structure here. */
    public TimeMap() {
        datamap=new HashMap<>();
            
    }
    
    public void set(String key, String value, int timestamp) {
        Map<Integer,String> map=datamap.getOrDefault(key,new HashMap<Integer,String>());
        map.put(timestamp,value);
        datamap.put(key, map);
        // System.out.println(datamap);
    }
    
    private int getTimestampKey(Map<Integer,String> map, int timestamp) {
        if (map.isEmpty()) return -1;
        List<Integer> keys=new ArrayList<>(map.keySet());
        Collections.sort(keys);
        if (keys.get(0)>timestamp) 
            return -1;
        int idx=(keys.size()-1)/2;
        while(idx>=0 && idx<keys.size()) {
            int ts=keys.get(idx);
            if (ts<timestamp) {
                if (idx == keys.size()-1 || (idx < (keys.size()-1) && keys.get(idx+1)>timestamp))
                    return ts;
                else
                    idx++;
            } else if (ts==timestamp) {
                return ts;
            } else {
                idx--;
            }
        }
        return -1;
    }
    
    public String get(String key, int timestamp) {
        Map<Integer,String> map=datamap.getOrDefault(key, new HashMap<Integer,String>());
        return map.getOrDefault(getTimestampKey(map, timestamp),"");
    }
}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
```