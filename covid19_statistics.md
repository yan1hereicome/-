def normalize_data(n_cases, n_people, scale):
    norm_cases = []
    for idx, n in enumerate(n_cases):
        norm_cases.append((n / n_people[idx]) * scale)
    return norm_cases

regions  = ['Seoul', 'Gyeongi', 'Busan', 'Gyeongnam', 'Incheon', 'Gyeongbuk', 'Daegu', 'Chungnam', 'Jeonnam', 'Jeonbuk', 'Chungbuk', 'Gangwon', 'Daejeon', 'Gwangju', 'Ulsan', 'Jeju', 'Sejong']
n_people = [9550227,  13530519, 3359527,     3322373,   2938429,     2630254, 2393626,    2118183,   1838353,   1792476,    1597179,   1536270,   1454679,   1441970, 1124459, 675883,   365309] # 2021-08
n_covid  = [    644,       529,      38,          29,       148,          28,      41,         62,        23,        27,         27,        33,        16,        40,      20,      5,        4] # 2021-09-21

sum_people = sum(n_people)#TODO) The total  number of people
print('### Korean Population by Region')
print('* Total population:', sum_people)
print() # Print an empty line
print('| Region | Population | Ratio (%) |')
print('| ------ | ---------- | --------- |')
sum_covid = sum(n_covid)#TODO) the total number of newcases 
for idx, pop in enumerate(n_people):
    ratio = (n_covid[idx] / sum_covid) * 100
    print('| %s | %d | %.1f |' % (regions[idx], pop, ratio))
print()

norm_covid = normalize_data(n_covid, n_people, 1000000)
print()
print('### COVID-19 New Cases by Region',sum_covid)
print('| Region |Ratio(%)| New Cases per 1M People |')
print('| ------ | --------------------- |')
for idx, norm_case in enumerate(norm_covid):
    total_cases = n_covid[idx]  # assuming n_covid is a list of total cases for each region
    ratio = (norm_case / total_cases) * 100
    print('| %s | %.1f | %d |' % (regions[idx], ratio, norm_case))
