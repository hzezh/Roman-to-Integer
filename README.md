# Roman-to-Integer
class Solution:
    def romanToInt(self, input_str: str) -> int:
        roman_map = {
          "I": 1,
          "V": 5,
          "X": 10,
          "L": 50,
          "C": 100,
          "D": 500,
          "M": 1000
        }
        length_Str = len(input_str)

        sum = 0
        should_skip = False

        for index in range(0,length_Str):
          if should_skip == True:
            should_skip = False
            #print ('skipping')
            continue

          current= input_str[index]

          #print(sum)
          if index == length_Str - 1:
            sum = sum + roman_map[current]
            should_skip = False
            #print(f'for last {sum}')
            break

          if current == 'I':
            next = input_str[index+1]
            if next == 'V' or next == 'X':
              sum = sum + roman_map[next] - roman_map[current]
              should_skip = True
              #print(f'for I {sum}')
            else:
              sum = sum + roman_map[current]


          elif current == 'C':
            next = input_str[index+1]
            if next == 'D' or next == 'M':
              sum = sum + roman_map[next] - roman_map[current]
              should_skip = True
              #print(f'for C {sum}')
            else:
              sum = sum + roman_map[current]

          elif current == 'X':
            should_skip = False
            next = input_str[index+1]
            if next == 'L' or next == 'C':
              sum = sum + roman_map[next] - roman_map[current]
              should_skip = True
              #print(f'for X {sum}')
            else:
              sum = sum + roman_map[current]
              #print(f'for X else {sum}')


          else:
            #print('regular scenario')
            sum = sum + roman_map[current]
        return sum
