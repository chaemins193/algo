https://programmers.co.kr/learn/courses/30/lessons/43164
``` java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
class Solution {
    List<String> list = new ArrayList<>();
	static String route = "";
	static boolean[] visit;
	
	private void dfs(String[][] tickets, String end, int cnt) {
		route += end + ",";
		
		if(cnt == tickets.length) {
			list.add(route); return;
		}
		
		for(int i = 0; i < tickets.length; i++) {
			String s = tickets[i][0], e = tickets[i][1];
			if(s.equals(end) && !visit[i]) {
				visit[i] = true;
				dfs(tickets, e, cnt + 1);
				visit[i] = false; route = route.substring(0, route.length()-4);
			}
		}
	}
	
	public String[] solution(String[][] tickets) {
		for(int i = 0; i < tickets.length; i++) {
			visit = new boolean[tickets.length];
			String start = tickets[i][0], end = tickets[i][1];
			
			if(start.equals("ICN")) {
				route = start + ","; visit[i] = true; 
				dfs(tickets, end, 1);
			}
		}
		
		Collections.sort(list);
		String[] answer = list.get(0).split(",");

		return answer;
	}
}
