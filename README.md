

def convert_integer_types():

    hex_to_bin_table = {'0':'0000', '1':'0001', '2':'0010','3':'0011', '4': '0100', '5': '0101', '6':'0110', '7': '0111', '8': '1000', '9': '1001', 'A': '1010', 'B': '1011', 'C': '1100', 'D': '1101', 'E': '1110', 'F': '1111'}
    hex_to_bin_table_l1 = {'0':'000', '1':'001', '2':'010','3':'011', '4': '100', '5': '101', '6':'110', '7': '111', '8': '1000', '9': '1001', 'A': '1010', 'B': '1011', 'C': '1100', 'D': '1101', 'E': '1110', 'F': '1111'}
    hex_to_bin_table_l2 = {'0':'00', '1':'01', '2':'10','3':'11', '4': '100', '5': '101', '6':'110', '7': '111', '8': '1000', '9': '1001', 'A': '1010', 'B': '1011', 'C': '1100', 'D': '1101', 'E': '1110', 'F': '1111'}
    hex_to_bin_table_l3 = {'0':'0', '1':'1', '2':'10','3':'11', '4': '100', '5': '101', '6':'110', '7': '111', '8': '1000', '9': '1001', 'A': '1010', 'B': '1011', 'C': '1100', 'D': '1101', 'E': '1110', 'F': '1111'}
    bin_to_hex_table = dict([(x[1] , x[0]) for x in zip(hex_to_bin_table.keys(), hex_to_bin_table.values())])
    
    


    #Receive type of conversion
    def rec_conv_type():
        print("for Decimal to Binary type DB" + "\n")
        print("for Binary to Decimal type BD" + "\n")
        print("for Binary to Hexadecimal type BH" + "\n")
        print("for Hexadecimal to Binary type HB" + "\n")
        global task 
        task = input().lower()
        global name_eror
        name_eror = False

    rec_conv_type()
    #Print to user what he has choosen and identify name Eror
    def print_conv_type():
        if task == "db":
            print("Decimal to Binary chosen" + "\n")
        elif task == "bd":
            print("Binary to Decimal chosen")
        elif task == "bh":
            print("Binary to Hexadecimal chosen")
        elif task == "hb":
            print("Hexadecimal to Binary chosen")
        elif task == "dh":
            print("Decimal to Hexadecimal chosen")
        elif task == "hd":
            print("Hexadecimal to Decimal chosen")
        else:
            print("Unsuported opperation or mistype, please try again")
            global name_eror
            name_eror = True 

    print_conv_type()
    #Check mistype
    def check_answer_fun():
        check_answer = input("If you want to change conversion type, type 'abort'" +  "\n" "If not just type any letter" + "\n").lower()
        while check_answer == "abort":
            print("\n" * 5)
            rec_conv_type()
            print_conv_type()
            if name_eror == True:
                continue
            check_answer = input("If you want to change conversion type, type 'abort'" +  "\n" "If not just type any letter" + "\n").lower()
  #Makes binary numbers prety   
    def sort_converted_numbers_in_DB(lst_bin):
        fin_lst= []
        for bin in lst_bin:
            bin_norm = ""
            try:
                bin = bin.split(".")
                for el in reversed(bin):
                    if el == "0":
                        alpha = "omega"
                    elif el == "01":
                        bin_norm += "1"
                    elif el == "1":
                        bin_norm += "1"
                    else:
                        bin_norm += "0"
                if bin[len(bin)-1] == "0":
                    bin_norm += "0"
            except:
                fin_lst.append(bin)
            fin_lst.append(bin_norm)
        return fin_lst 



    #Conversion Functions
    def decimal_to_binary():
        user_input = None
        global list_of_decimal_numbs
        list_of_decimal_numbs = []
        while user_input != "abort":
            user_input = input("Type number to convert, if you finished type 'abort'" + "\n")
            try:
                user_input.isnumeric
                list_of_decimal_numbs.append(user_input)
            except:
                continue
        converted_numbers = []
        list_of_decimal_numbs.remove("abort")
        for num in list_of_decimal_numbs:
            num = int(num)
            converted_number = ""
            while num != 1:
                it = num % 2
                if it == 1:
                     num = (num - 1)/2
                else:
                     num = num/2
                converted_number += str(it)
            it = num % 2
            if it == 1:
                 num = (num - 1)/2
            else:
                num = num/2
            converted_number += str(it)
            converted_numbers.append(converted_number)
        converted_numbers = sort_converted_numbers_in_DB(converted_numbers)
        return converted_numbers

        
    def binary_to_decimal():
         user_input = None
         global list_of_binary_numbs
         list_of_binary_numbs = []
         while user_input != "abort":
             user_input = input("Type number to convert, if you finished type 'abort'" + "\n")
             try:
                 int(user_input)
                 list_of_binary_numbs.append(user_input)
             except:
                 continue
         converted_numbers = []
         for num in list_of_binary_numbs:
             bin_num_in_lst = []
             for el in num:
                 bin_num_in_lst.append(el)
             enc = 0
             total = 0
             for part in reversed(bin_num_in_lst):
                 if part == "0":
                     Alpha = 'omega'
                 else:
                     total += 2 ** enc
                 enc += 1 
             converted_numbers.append(total)
         return converted_numbers


    def binary_to_Hex():
         user_input = None
         global list_of_binary_numbs_for_BH
         list_of_binary_numbs_for_BH = []
         while user_input != "abort":
             user_input = input("Type number to convert, if you finished type 'abort'" + "\n" + "#NOTE binary number must be x % 4 == 0 " + "\n" + "\n")
             try:
                 int(user_input)
                 list_of_binary_numbs_for_BH.append(user_input)
             except:
                 continue
         converted_numbers = []
         for num in list_of_binary_numbs_for_BH:
             x = 0
             converted_number = ""
             for four_count in range(int(len(num))//4):
                 converted_four = bin_to_hex_table [ num[x : x + 4] ]
                 print(converted_four)
                 x += 4
                 converted_number += converted_four
             converted_numbers.append(converted_number)
         return converted_numbers



    def hex_to_Binary():
         user_input = None
         global list_of_binary_numbs_for_HB
         list_of_binary_numbs_for_HB = []
         while user_input != "ABORT":
             if user_input == "ABORT":
                 break
             user_input = input("Type number equivavelnt in HEX to convert, if you finished type 'abort'" + "\n" + "\n")
             try:
                 user_input = user_input.upper()
                 list_of_binary_numbs_for_HB.append(user_input)
             except:
                 continue
         converted_numbers = []
         list_of_binary_numbs_for_HB.remove("ABORT")
         for num in list_of_binary_numbs_for_HB:
             print(num)
             num_converted = ""
             for el in num:
                 print(el)
                 num_converted += hex_to_bin_table[el]
             converted_numbers.append(num_converted)
         return converted_numbers


        
    #Report Name Error and execute conversion
    if name_eror == False:  
        check_answer_fun()
        if task == "db":
            answer = decimal_to_binary()
            for DB_answer in zip(answer , list_of_decimal_numbs):
                print("Number {} in binary is {}".format(DB_answer[1] , DB_answer[0]) + "\n")
        elif task == "bd":
            answer = binary_to_decimal()
            for BD_answer in zip(answer, list_of_binary_numbs):
                print("Number {} in decimal is {}".format(BD_answer[1] , BD_answer[0]) + "\n")
        elif task == "bh":
            answer = binary_to_Hex()
            for BH_answer in zip(answer, list_of_binary_numbs_for_BH):
                print("Number {} in Hexadecimal is {}".format(BH_answer[1] , BH_answer[0]) + "\n")
        elif task == "hb":
            answer = hex_to_Binary()
            for HB_answer in zip(answer, list_of_binary_numbs_for_HB):
                print("Number {} in Hexadecimal is {}".format(HB_answer[1] , HB_answer[0]) + "\n")
    else:
        return "Name Error"


convert_integer_types()
