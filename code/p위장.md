``` java
import java.util.*;

class Solution {
    public int solution(String[][] clothes) {
        int answer = 1;
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        for(int i=0;i<clothes.length;i++){
            if(map.containsKey(clothes[i][1])){ // 해당 종류의 키가 이미 있을 경우
                map.put(clothes[i][1], map.get(clothes[i][1])+1);
            }
            else{// 해당 종류의 키가 없을 경우
                map.put(clothes[i][1], 1);
            }
        }
        for(int val : map.values()){
            answer *= (val + 1); // 해당 종류의 옷을 안 입을 수도 있기 때문에 +1
        }
        return answer-1; // 아무것도 착용 안한 경우 제외
    }
}
