``` java
import java.util.*;

class Solution {
    public int solution(int N, int number) {
        int answer = -1;
        //다음 단계에서 재사용하기 위해 각 단계에서 계산된 결과 저장
        //N의 사용 횟수, [계산 결과 목록]
        HashMap<Integer, HashSet<Integer>> map = new HashMap<>();
        HashSet<Integer> s = new HashSet<>();
        s.add(N); //N 한 개만 사용하는 경우 미리 저장
        map.put(1, s);
        //중첩 반복문
        loop : for (int i = 2; i < 9; i++) { // N을 8번 사용할 때까지 탐색(NN, NNN, ~)
            HashSet<Integer> set = new LinkedHashSet<>();

            int NNN = Integer.parseInt(Integer.toBinaryString((int) Math.pow(2, i) - 1)) * N;

            if (NNN == number){
                return i;
            }

            set.add(NNN); //DP 컬렉션에 추가

            for (int j = 1; j <= i / 2; j++) {
                Iterator<Integer> it1 = map.get(j).iterator();
                Iterator<Integer> it2 = map.get(i - j).iterator();

                while (it1.hasNext()) {
                    int itValue1 = it1.next();
                    while (it2.hasNext()) {
                        int itValue2 = it2.next();
                        for (Operator o : Operator.values()) {
                            int calculate = o.calculate(itValue1, itValue2);
                            if (calculate == number){
                                answer = i;
                                break loop;
                            }

                            set.add(calculate);
                        }
                    }
                }
            }
            map.put(i, set);
        }

        return answer;
    }

    enum Operator {
        PLUS {
            @Override
            public int calculate(int i, int j) {
                return i + j;
            }
        }, MINUS {
            @Override
            public int calculate(int i, int j) {
                return i - j;
            }
        }, BACKMINUS {
            @Override
            public int calculate(int i, int j) {
                return j - i;
            }
        }, MUL {
            @Override
            public int calculate(int i, int j) {
                return i * j;
            }
        }, DIV {
            @Override
            public int calculate(int i, int j) {
                if (j == 0){
                    return 0;
                }
                return i / j;
            }
        }, BACKDIV {
            @Override
            public int calculate(int i, int j) {
                if (i == 0){
                    return 0;
                }
                return j / i;
            }
        };

        public abstract int calculate(int i, int j);
    }
}
