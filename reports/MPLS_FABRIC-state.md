
# Validate State Report

**Table of Contents:**

- [Validate State Report](validate-state-report)
  - [Test Results Summary](#test-results-summary)
  - [Failed Test Results Summary](#failed-test-results-summary)
  - [All Test Results](#all-test-results)

## Test Results Summary

### Summary Totals

| Total Tests | Total Tests Passed | Total Tests Failed |
| ----------- | ------------------ | ------------------ |
| 396 | 341 | 55 |

### Summary Totals Devices Under Tests

| DUT | Total Tests | Tests Passed | Tests Failed | Categories Failed |
| --- | ----------- | ------------ | ------------ | ----------------- |
| P-01 |  64 | 57 | 7 | Hardware, NTP |
| P-02 |  67 | 65 | 2 | Hardware, NTP |
| PE-01 |  56 | 40 | 16 | Hardware, NTP |
| PE-02 |  78 | 71 | 7 | Hardware, NTP |
| PE-03 |  74 | 65 | 9 | Hardware, NTP |
| PE-04 |  57 | 43 | 14 | Hardware, NTP, Interface State |

### Summary Totals Per Category

| Test Category | Total Tests | Tests Passed | Tests Failed |
| ------------- | ----------- | ------------ | ------------ |
| Hardware |  304 | 256 | 48 |
| NTP |  6 | 0 | 6 |
| Interface State |  28 | 27 | 1 |
| LLDP Topology |  18 | 18 | 0 |
| IP Reachability |  18 | 18 | 0 |
| BGP |  22 | 22 | 0 |

## Failed Test Results Summary

| Test ID | Node | Test Category | Test Description | Test | Test Result | Failure Reason |
| ------- | ---- | ------------- | ---------------- | ---- | ----------- | -------------- |
| 2 | P-01 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 4 | P-02 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 6 | PE-01 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 7 | PE-02 | Hardware | Power supply state | Power supply 1 | FAIL | Power supply state is "powerLoss" |
| 9 | PE-03 | Hardware | Power supply state | Power supply 1 | FAIL | Power supply state is "powerLoss" |
| 12 | PE-04 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 57 | P-01 | Hardware | transceivers manufacturers | port 23 | FAIL | transceivers manufacturers is "Arista Networks " |
| 59 | P-01 | Hardware | transceivers manufacturers | port 25 | FAIL | transceivers manufacturers is "Arista Networks " |
| 60 | P-01 | Hardware | transceivers manufacturers | port 26 | FAIL | transceivers manufacturers is "Arista Networks " |
| 74 | P-01 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 77 | P-01 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 121 | PE-01 | Hardware | transceivers manufacturers | port 11 | FAIL | transceivers manufacturers is "Arista Networks " |
| 122 | PE-01 | Hardware | transceivers manufacturers | port 10 | FAIL | transceivers manufacturers is "Arista Networks " |
| 127 | PE-01 | Hardware | transceivers manufacturers | port 17 | FAIL | transceivers manufacturers is "CISCO-SUMITOMO  " |
| 128 | PE-01 | Hardware | transceivers manufacturers | port 15 | FAIL | transceivers manufacturers is "Arista Networks " |
| 132 | PE-01 | Hardware | transceivers manufacturers | port 26 | FAIL | transceivers manufacturers is "Arista Networks " |
| 139 | PE-01 | Hardware | transceivers manufacturers | port 32 | FAIL | transceivers manufacturers is "Arista Networks " |
| 140 | PE-01 | Hardware | transceivers manufacturers | port 31 | FAIL | transceivers manufacturers is "Arista Networks " |
| 146 | PE-01 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 149 | PE-01 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 150 | PE-01 | Hardware | transceivers manufacturers | port 5 | FAIL | transceivers manufacturers is "Arista Networks " |
| 151 | PE-01 | Hardware | transceivers manufacturers | port 4 | FAIL | transceivers manufacturers is "Arista Networks " |
| 152 | PE-01 | Hardware | transceivers manufacturers | port 7 | FAIL | transceivers manufacturers is "Arista Networks " |
| 154 | PE-01 | Hardware | transceivers manufacturers | port 9 | FAIL | transceivers manufacturers is "Arista Networks " |
| 155 | PE-01 | Hardware | transceivers manufacturers | port 8 | FAIL | transceivers manufacturers is "Arista Networks " |
| 201 | PE-02 | Hardware | transceivers manufacturers | port 54 | FAIL | transceivers manufacturers is "Arista Networks " |
| 203 | PE-02 | Hardware | transceivers manufacturers | port 49 | FAIL | transceivers manufacturers is "Arista Networks " |
| 207 | PE-02 | Hardware | transceivers manufacturers | port 52 | FAIL | transceivers manufacturers is "Arista Networks " |
| 209 | PE-02 | Hardware | transceivers manufacturers | port 55 | FAIL | transceivers manufacturers is "Arista Networks " |
| 212 | PE-02 | Hardware | transceivers manufacturers | port 50 | FAIL | transceivers manufacturers is "Arista Networks " |
| 234 | PE-03 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 236 | PE-03 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 257 | PE-03 | Hardware | transceivers manufacturers | port 54 | FAIL | transceivers manufacturers is "Arista Networks " |
| 260 | PE-03 | Hardware | transceivers manufacturers | port 51 | FAIL | transceivers manufacturers is "Arista Networks " |
| 262 | PE-03 | Hardware | transceivers manufacturers | port 53 | FAIL | transceivers manufacturers is "Arista Networks " |
| 265 | PE-03 | Hardware | transceivers manufacturers | port 55 | FAIL | transceivers manufacturers is "Arista Networks " |
| 268 | PE-03 | Hardware | transceivers manufacturers | port 50 | FAIL | transceivers manufacturers is "Arista Networks " |
| 269 | PE-04 | Hardware | transceivers manufacturers | port 11 | FAIL | transceivers manufacturers is "Arista Networks " |
| 270 | PE-04 | Hardware | transceivers manufacturers | port 10 | FAIL | transceivers manufacturers is "Arista Networks " |
| 276 | PE-04 | Hardware | transceivers manufacturers | port 15 | FAIL | transceivers manufacturers is "Arista Networks " |
| 285 | PE-04 | Hardware | transceivers manufacturers | port 16 | FAIL | transceivers manufacturers is "Arista Networks " |
| 294 | PE-04 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 296 | PE-04 | Hardware | transceivers manufacturers | port 3 | FAIL | transceivers manufacturers is "Arista Networks " |
| 297 | PE-04 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 298 | PE-04 | Hardware | transceivers manufacturers | port 5 | FAIL | transceivers manufacturers is "Arista Networks " |
| 300 | PE-04 | Hardware | transceivers manufacturers | port 7 | FAIL | transceivers manufacturers is "Arista Networks " |
| 302 | PE-04 | Hardware | transceivers manufacturers | port 9 | FAIL | transceivers manufacturers is "Arista Networks " |
| 303 | PE-04 | Hardware | transceivers manufacturers | port 8 | FAIL | transceivers manufacturers is "Arista Networks " |
| 305 | P-01 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 306 | P-02 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 307 | PE-01 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 308 | PE-02 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 309 | PE-03 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 310 | PE-04 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 332 | PE-04 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet5/1 - speed_config_10g | FAIL | interface status: down - line protocol status: down |

## All Test Results

| Test ID | Node | Test Category | Test Description | Test | Test Result | Failure Reason |
| ------- | ---- | ------------- | ---------------- | ---- | ----------- | -------------- |
| 1 | P-01 | Hardware | Power supply state | Power supply 1 | PASS |  |
| 2 | P-01 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 3 | P-02 | Hardware | Power supply state | Power supply 1 | PASS |  |
| 4 | P-02 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 5 | PE-01 | Hardware | Power supply state | Power supply 1 | PASS |  |
| 6 | PE-01 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 7 | PE-02 | Hardware | Power supply state | Power supply 1 | FAIL | Power supply state is "powerLoss" |
| 8 | PE-02 | Hardware | Power supply state | Power supply 2 | PASS |  |
| 9 | PE-03 | Hardware | Power supply state | Power supply 1 | FAIL | Power supply state is "powerLoss" |
| 10 | PE-03 | Hardware | Power supply state | Power supply 2 | PASS |  |
| 11 | PE-04 | Hardware | Power supply state | Power supply 1 | PASS |  |
| 12 | PE-04 | Hardware | Power supply state | Power supply 2 | FAIL | Power supply state is "powerLoss" |
| 13 | P-01 | Hardware | fan status (power supplies) | PowerSupply1 | PASS |  |
| 14 | P-01 | Hardware | fan status (power supplies) | PowerSupply2 | PASS |  |
| 15 | P-02 | Hardware | fan status (power supplies) | PowerSupply1 | PASS |  |
| 16 | P-02 | Hardware | fan status (power supplies) | PowerSupply2 | PASS |  |
| 17 | PE-01 | Hardware | fan status (power supplies) | PowerSupply1 | PASS |  |
| 18 | PE-01 | Hardware | fan status (power supplies) | PowerSupply2 | PASS |  |
| 19 | PE-02 | Hardware | fan status (power supplies) | PowerSupply1 | PASS |  |
| 20 | PE-02 | Hardware | fan status (power supplies) | PowerSupply2 | PASS |  |
| 21 | PE-03 | Hardware | fan status (power supplies) | PowerSupply1 | PASS |  |
| 22 | PE-03 | Hardware | fan status (power supplies) | PowerSupply2 | PASS |  |
| 23 | PE-04 | Hardware | fan status (power supplies) | PowerSupply1 | PASS |  |
| 24 | PE-04 | Hardware | fan status (power supplies) | PowerSupply2 | PASS |  |
| 25 | P-01 | Hardware | fan status (fan tray) | Tray 1 | PASS |  |
| 26 | P-01 | Hardware | fan status (fan tray) | Tray 2 | PASS |  |
| 27 | P-01 | Hardware | fan status (fan tray) | Tray 3 | PASS |  |
| 28 | P-01 | Hardware | fan status (fan tray) | Tray 4 | PASS |  |
| 29 | P-02 | Hardware | fan status (fan tray) | Tray 1 | PASS |  |
| 30 | P-02 | Hardware | fan status (fan tray) | Tray 2 | PASS |  |
| 31 | P-02 | Hardware | fan status (fan tray) | Tray 3 | PASS |  |
| 32 | P-02 | Hardware | fan status (fan tray) | Tray 4 | PASS |  |
| 33 | PE-01 | Hardware | fan status (fan tray) | Tray 1 | PASS |  |
| 34 | PE-01 | Hardware | fan status (fan tray) | Tray 2 | PASS |  |
| 35 | PE-01 | Hardware | fan status (fan tray) | Tray 3 | PASS |  |
| 36 | PE-02 | Hardware | fan status (fan tray) | Tray 1 | PASS |  |
| 37 | PE-02 | Hardware | fan status (fan tray) | Tray 2 | PASS |  |
| 38 | PE-03 | Hardware | fan status (fan tray) | Tray 1 | PASS |  |
| 39 | PE-03 | Hardware | fan status (fan tray) | Tray 2 | PASS |  |
| 40 | PE-04 | Hardware | fan status (fan tray) | Tray 1 | PASS |  |
| 41 | PE-04 | Hardware | fan status (fan tray) | Tray 2 | PASS |  |
| 42 | PE-04 | Hardware | fan status (fan tray) | Tray 3 | PASS |  |
| 43 | P-01 | Hardware | temperature | system temperature | PASS |  |
| 44 | P-02 | Hardware | temperature | system temperature | PASS |  |
| 45 | PE-01 | Hardware | temperature | system temperature | PASS |  |
| 46 | PE-02 | Hardware | temperature | system temperature | PASS |  |
| 47 | PE-03 | Hardware | temperature | system temperature | PASS |  |
| 48 | PE-04 | Hardware | temperature | system temperature | PASS |  |
| 49 | P-01 | Hardware | transceivers manufacturers | port 11 | PASS |  |
| 50 | P-01 | Hardware | transceivers manufacturers | port 10 | PASS |  |
| 51 | P-01 | Hardware | transceivers manufacturers | port 6 | PASS |  |
| 52 | P-01 | Hardware | transceivers manufacturers | port 13 | PASS |  |
| 53 | P-01 | Hardware | transceivers manufacturers | port 29 | PASS |  |
| 54 | P-01 | Hardware | transceivers manufacturers | port 12 | PASS |  |
| 55 | P-01 | Hardware | transceivers manufacturers | port 17 | PASS |  |
| 56 | P-01 | Hardware | transceivers manufacturers | port 15 | PASS |  |
| 57 | P-01 | Hardware | transceivers manufacturers | port 23 | FAIL | transceivers manufacturers is "Arista Networks " |
| 58 | P-01 | Hardware | transceivers manufacturers | port 24 | PASS |  |
| 59 | P-01 | Hardware | transceivers manufacturers | port 25 | FAIL | transceivers manufacturers is "Arista Networks " |
| 60 | P-01 | Hardware | transceivers manufacturers | port 26 | FAIL | transceivers manufacturers is "Arista Networks " |
| 61 | P-01 | Hardware | transceivers manufacturers | port 27 | PASS |  |
| 62 | P-01 | Hardware | transceivers manufacturers | port 20 | PASS |  |
| 63 | P-01 | Hardware | transceivers manufacturers | port 21 | PASS |  |
| 64 | P-01 | Hardware | transceivers manufacturers | port 22 | PASS |  |
| 65 | P-01 | Hardware | transceivers manufacturers | port 16 | PASS |  |
| 66 | P-01 | Hardware | transceivers manufacturers | port 19 | PASS |  |
| 67 | P-01 | Hardware | transceivers manufacturers | port 32 | PASS |  |
| 68 | P-01 | Hardware | transceivers manufacturers | port 31 | PASS |  |
| 69 | P-01 | Hardware | transceivers manufacturers | port 30 | PASS |  |
| 70 | P-01 | Hardware | transceivers manufacturers | port 28 | PASS |  |
| 71 | P-01 | Hardware | transceivers manufacturers | port 36 | PASS |  |
| 72 | P-01 | Hardware | transceivers manufacturers | port 35 | PASS |  |
| 73 | P-01 | Hardware | transceivers manufacturers | port 34 | PASS |  |
| 74 | P-01 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 75 | P-01 | Hardware | transceivers manufacturers | port 33 | PASS |  |
| 76 | P-01 | Hardware | transceivers manufacturers | port 3 | PASS |  |
| 77 | P-01 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 78 | P-01 | Hardware | transceivers manufacturers | port 5 | PASS |  |
| 79 | P-01 | Hardware | transceivers manufacturers | port 4 | PASS |  |
| 80 | P-01 | Hardware | transceivers manufacturers | port 7 | PASS |  |
| 81 | P-01 | Hardware | transceivers manufacturers | port 18 | PASS |  |
| 82 | P-01 | Hardware | transceivers manufacturers | port 9 | PASS |  |
| 83 | P-01 | Hardware | transceivers manufacturers | port 8 | PASS |  |
| 84 | P-01 | Hardware | transceivers manufacturers | port 14 | PASS |  |
| 85 | P-02 | Hardware | transceivers manufacturers | port 11 | PASS |  |
| 86 | P-02 | Hardware | transceivers manufacturers | port 10 | PASS |  |
| 87 | P-02 | Hardware | transceivers manufacturers | port 6 | PASS |  |
| 88 | P-02 | Hardware | transceivers manufacturers | port 13 | PASS |  |
| 89 | P-02 | Hardware | transceivers manufacturers | port 29 | PASS |  |
| 90 | P-02 | Hardware | transceivers manufacturers | port 12 | PASS |  |
| 91 | P-02 | Hardware | transceivers manufacturers | port 17 | PASS |  |
| 92 | P-02 | Hardware | transceivers manufacturers | port 15 | PASS |  |
| 93 | P-02 | Hardware | transceivers manufacturers | port 23 | PASS |  |
| 94 | P-02 | Hardware | transceivers manufacturers | port 24 | PASS |  |
| 95 | P-02 | Hardware | transceivers manufacturers | port 25 | PASS |  |
| 96 | P-02 | Hardware | transceivers manufacturers | port 26 | PASS |  |
| 97 | P-02 | Hardware | transceivers manufacturers | port 27 | PASS |  |
| 98 | P-02 | Hardware | transceivers manufacturers | port 20 | PASS |  |
| 99 | P-02 | Hardware | transceivers manufacturers | port 21 | PASS |  |
| 100 | P-02 | Hardware | transceivers manufacturers | port 22 | PASS |  |
| 101 | P-02 | Hardware | transceivers manufacturers | port 16 | PASS |  |
| 102 | P-02 | Hardware | transceivers manufacturers | port 19 | PASS |  |
| 103 | P-02 | Hardware | transceivers manufacturers | port 32 | PASS |  |
| 104 | P-02 | Hardware | transceivers manufacturers | port 31 | PASS |  |
| 105 | P-02 | Hardware | transceivers manufacturers | port 30 | PASS |  |
| 106 | P-02 | Hardware | transceivers manufacturers | port 28 | PASS |  |
| 107 | P-02 | Hardware | transceivers manufacturers | port 36 | PASS |  |
| 108 | P-02 | Hardware | transceivers manufacturers | port 35 | PASS |  |
| 109 | P-02 | Hardware | transceivers manufacturers | port 34 | PASS |  |
| 110 | P-02 | Hardware | transceivers manufacturers | port 1 | PASS |  |
| 111 | P-02 | Hardware | transceivers manufacturers | port 33 | PASS |  |
| 112 | P-02 | Hardware | transceivers manufacturers | port 3 | PASS |  |
| 113 | P-02 | Hardware | transceivers manufacturers | port 2 | PASS |  |
| 114 | P-02 | Hardware | transceivers manufacturers | port 5 | PASS |  |
| 115 | P-02 | Hardware | transceivers manufacturers | port 4 | PASS |  |
| 116 | P-02 | Hardware | transceivers manufacturers | port 7 | PASS |  |
| 117 | P-02 | Hardware | transceivers manufacturers | port 18 | PASS |  |
| 118 | P-02 | Hardware | transceivers manufacturers | port 9 | PASS |  |
| 119 | P-02 | Hardware | transceivers manufacturers | port 8 | PASS |  |
| 120 | P-02 | Hardware | transceivers manufacturers | port 14 | PASS |  |
| 121 | PE-01 | Hardware | transceivers manufacturers | port 11 | FAIL | transceivers manufacturers is "Arista Networks " |
| 122 | PE-01 | Hardware | transceivers manufacturers | port 10 | FAIL | transceivers manufacturers is "Arista Networks " |
| 123 | PE-01 | Hardware | transceivers manufacturers | port 6 | PASS |  |
| 124 | PE-01 | Hardware | transceivers manufacturers | port 13 | PASS |  |
| 125 | PE-01 | Hardware | transceivers manufacturers | port 29 | PASS |  |
| 126 | PE-01 | Hardware | transceivers manufacturers | port 12 | PASS |  |
| 127 | PE-01 | Hardware | transceivers manufacturers | port 17 | FAIL | transceivers manufacturers is "CISCO-SUMITOMO  " |
| 128 | PE-01 | Hardware | transceivers manufacturers | port 15 | FAIL | transceivers manufacturers is "Arista Networks " |
| 129 | PE-01 | Hardware | transceivers manufacturers | port 23 | PASS |  |
| 130 | PE-01 | Hardware | transceivers manufacturers | port 24 | PASS |  |
| 131 | PE-01 | Hardware | transceivers manufacturers | port 25 | PASS |  |
| 132 | PE-01 | Hardware | transceivers manufacturers | port 26 | FAIL | transceivers manufacturers is "Arista Networks " |
| 133 | PE-01 | Hardware | transceivers manufacturers | port 27 | PASS |  |
| 134 | PE-01 | Hardware | transceivers manufacturers | port 20 | PASS |  |
| 135 | PE-01 | Hardware | transceivers manufacturers | port 21 | PASS |  |
| 136 | PE-01 | Hardware | transceivers manufacturers | port 22 | PASS |  |
| 137 | PE-01 | Hardware | transceivers manufacturers | port 16 | PASS |  |
| 138 | PE-01 | Hardware | transceivers manufacturers | port 19 | PASS |  |
| 139 | PE-01 | Hardware | transceivers manufacturers | port 32 | FAIL | transceivers manufacturers is "Arista Networks " |
| 140 | PE-01 | Hardware | transceivers manufacturers | port 31 | FAIL | transceivers manufacturers is "Arista Networks " |
| 141 | PE-01 | Hardware | transceivers manufacturers | port 30 | PASS |  |
| 142 | PE-01 | Hardware | transceivers manufacturers | port 28 | PASS |  |
| 143 | PE-01 | Hardware | transceivers manufacturers | port 36 | PASS |  |
| 144 | PE-01 | Hardware | transceivers manufacturers | port 35 | PASS |  |
| 145 | PE-01 | Hardware | transceivers manufacturers | port 34 | PASS |  |
| 146 | PE-01 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 147 | PE-01 | Hardware | transceivers manufacturers | port 33 | PASS |  |
| 148 | PE-01 | Hardware | transceivers manufacturers | port 3 | PASS |  |
| 149 | PE-01 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 150 | PE-01 | Hardware | transceivers manufacturers | port 5 | FAIL | transceivers manufacturers is "Arista Networks " |
| 151 | PE-01 | Hardware | transceivers manufacturers | port 4 | FAIL | transceivers manufacturers is "Arista Networks " |
| 152 | PE-01 | Hardware | transceivers manufacturers | port 7 | FAIL | transceivers manufacturers is "Arista Networks " |
| 153 | PE-01 | Hardware | transceivers manufacturers | port 18 | PASS |  |
| 154 | PE-01 | Hardware | transceivers manufacturers | port 9 | FAIL | transceivers manufacturers is "Arista Networks " |
| 155 | PE-01 | Hardware | transceivers manufacturers | port 8 | FAIL | transceivers manufacturers is "Arista Networks " |
| 156 | PE-01 | Hardware | transceivers manufacturers | port 14 | PASS |  |
| 157 | PE-02 | Hardware | transceivers manufacturers | port 56 | PASS |  |
| 158 | PE-02 | Hardware | transceivers manufacturers | port 28 | PASS |  |
| 159 | PE-02 | Hardware | transceivers manufacturers | port 29 | PASS |  |
| 160 | PE-02 | Hardware | transceivers manufacturers | port 35 | PASS |  |
| 161 | PE-02 | Hardware | transceivers manufacturers | port 34 | PASS |  |
| 162 | PE-02 | Hardware | transceivers manufacturers | port 24 | PASS |  |
| 163 | PE-02 | Hardware | transceivers manufacturers | port 25 | PASS |  |
| 164 | PE-02 | Hardware | transceivers manufacturers | port 26 | PASS |  |
| 165 | PE-02 | Hardware | transceivers manufacturers | port 27 | PASS |  |
| 166 | PE-02 | Hardware | transceivers manufacturers | port 20 | PASS |  |
| 167 | PE-02 | Hardware | transceivers manufacturers | port 21 | PASS |  |
| 168 | PE-02 | Hardware | transceivers manufacturers | port 22 | PASS |  |
| 169 | PE-02 | Hardware | transceivers manufacturers | port 23 | PASS |  |
| 170 | PE-02 | Hardware | transceivers manufacturers | port 46 | PASS |  |
| 171 | PE-02 | Hardware | transceivers manufacturers | port 47 | PASS |  |
| 172 | PE-02 | Hardware | transceivers manufacturers | port 44 | PASS |  |
| 173 | PE-02 | Hardware | transceivers manufacturers | port 45 | PASS |  |
| 174 | PE-02 | Hardware | transceivers manufacturers | port 42 | PASS |  |
| 175 | PE-02 | Hardware | transceivers manufacturers | port 43 | PASS |  |
| 176 | PE-02 | Hardware | transceivers manufacturers | port 40 | PASS |  |
| 177 | PE-02 | Hardware | transceivers manufacturers | port 41 | PASS |  |
| 178 | PE-02 | Hardware | transceivers manufacturers | port 1 | PASS |  |
| 179 | PE-02 | Hardware | transceivers manufacturers | port 3 | PASS |  |
| 180 | PE-02 | Hardware | transceivers manufacturers | port 2 | PASS |  |
| 181 | PE-02 | Hardware | transceivers manufacturers | port 5 | PASS |  |
| 182 | PE-02 | Hardware | transceivers manufacturers | port 4 | PASS |  |
| 183 | PE-02 | Hardware | transceivers manufacturers | port 7 | PASS |  |
| 184 | PE-02 | Hardware | transceivers manufacturers | port 6 | PASS |  |
| 185 | PE-02 | Hardware | transceivers manufacturers | port 9 | PASS |  |
| 186 | PE-02 | Hardware | transceivers manufacturers | port 8 | PASS |  |
| 187 | PE-02 | Hardware | transceivers manufacturers | port 18 | PASS |  |
| 188 | PE-02 | Hardware | transceivers manufacturers | port 13 | PASS |  |
| 189 | PE-02 | Hardware | transceivers manufacturers | port 38 | PASS |  |
| 190 | PE-02 | Hardware | transceivers manufacturers | port 30 | PASS |  |
| 191 | PE-02 | Hardware | transceivers manufacturers | port 14 | PASS |  |
| 192 | PE-02 | Hardware | transceivers manufacturers | port 11 | PASS |  |
| 193 | PE-02 | Hardware | transceivers manufacturers | port 10 | PASS |  |
| 194 | PE-02 | Hardware | transceivers manufacturers | port 39 | PASS |  |
| 195 | PE-02 | Hardware | transceivers manufacturers | port 12 | PASS |  |
| 196 | PE-02 | Hardware | transceivers manufacturers | port 15 | PASS |  |
| 197 | PE-02 | Hardware | transceivers manufacturers | port 48 | PASS |  |
| 198 | PE-02 | Hardware | transceivers manufacturers | port 17 | PASS |  |
| 199 | PE-02 | Hardware | transceivers manufacturers | port 16 | PASS |  |
| 200 | PE-02 | Hardware | transceivers manufacturers | port 19 | PASS |  |
| 201 | PE-02 | Hardware | transceivers manufacturers | port 54 | FAIL | transceivers manufacturers is "Arista Networks " |
| 202 | PE-02 | Hardware | transceivers manufacturers | port 31 | PASS |  |
| 203 | PE-02 | Hardware | transceivers manufacturers | port 49 | FAIL | transceivers manufacturers is "Arista Networks " |
| 204 | PE-02 | Hardware | transceivers manufacturers | port 51 | PASS |  |
| 205 | PE-02 | Hardware | transceivers manufacturers | port 36 | PASS |  |
| 206 | PE-02 | Hardware | transceivers manufacturers | port 53 | PASS |  |
| 207 | PE-02 | Hardware | transceivers manufacturers | port 52 | FAIL | transceivers manufacturers is "Arista Networks " |
| 208 | PE-02 | Hardware | transceivers manufacturers | port 33 | PASS |  |
| 209 | PE-02 | Hardware | transceivers manufacturers | port 55 | FAIL | transceivers manufacturers is "Arista Networks " |
| 210 | PE-02 | Hardware | transceivers manufacturers | port 37 | PASS |  |
| 211 | PE-02 | Hardware | transceivers manufacturers | port 32 | PASS |  |
| 212 | PE-02 | Hardware | transceivers manufacturers | port 50 | FAIL | transceivers manufacturers is "Arista Networks " |
| 213 | PE-03 | Hardware | transceivers manufacturers | port 56 | PASS |  |
| 214 | PE-03 | Hardware | transceivers manufacturers | port 28 | PASS |  |
| 215 | PE-03 | Hardware | transceivers manufacturers | port 29 | PASS |  |
| 216 | PE-03 | Hardware | transceivers manufacturers | port 35 | PASS |  |
| 217 | PE-03 | Hardware | transceivers manufacturers | port 34 | PASS |  |
| 218 | PE-03 | Hardware | transceivers manufacturers | port 24 | PASS |  |
| 219 | PE-03 | Hardware | transceivers manufacturers | port 25 | PASS |  |
| 220 | PE-03 | Hardware | transceivers manufacturers | port 26 | PASS |  |
| 221 | PE-03 | Hardware | transceivers manufacturers | port 27 | PASS |  |
| 222 | PE-03 | Hardware | transceivers manufacturers | port 20 | PASS |  |
| 223 | PE-03 | Hardware | transceivers manufacturers | port 21 | PASS |  |
| 224 | PE-03 | Hardware | transceivers manufacturers | port 22 | PASS |  |
| 225 | PE-03 | Hardware | transceivers manufacturers | port 23 | PASS |  |
| 226 | PE-03 | Hardware | transceivers manufacturers | port 46 | PASS |  |
| 227 | PE-03 | Hardware | transceivers manufacturers | port 47 | PASS |  |
| 228 | PE-03 | Hardware | transceivers manufacturers | port 44 | PASS |  |
| 229 | PE-03 | Hardware | transceivers manufacturers | port 45 | PASS |  |
| 230 | PE-03 | Hardware | transceivers manufacturers | port 42 | PASS |  |
| 231 | PE-03 | Hardware | transceivers manufacturers | port 43 | PASS |  |
| 232 | PE-03 | Hardware | transceivers manufacturers | port 40 | PASS |  |
| 233 | PE-03 | Hardware | transceivers manufacturers | port 41 | PASS |  |
| 234 | PE-03 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 235 | PE-03 | Hardware | transceivers manufacturers | port 3 | PASS |  |
| 236 | PE-03 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 237 | PE-03 | Hardware | transceivers manufacturers | port 5 | PASS |  |
| 238 | PE-03 | Hardware | transceivers manufacturers | port 4 | PASS |  |
| 239 | PE-03 | Hardware | transceivers manufacturers | port 7 | PASS |  |
| 240 | PE-03 | Hardware | transceivers manufacturers | port 6 | PASS |  |
| 241 | PE-03 | Hardware | transceivers manufacturers | port 9 | PASS |  |
| 242 | PE-03 | Hardware | transceivers manufacturers | port 8 | PASS |  |
| 243 | PE-03 | Hardware | transceivers manufacturers | port 18 | PASS |  |
| 244 | PE-03 | Hardware | transceivers manufacturers | port 13 | PASS |  |
| 245 | PE-03 | Hardware | transceivers manufacturers | port 38 | PASS |  |
| 246 | PE-03 | Hardware | transceivers manufacturers | port 30 | PASS |  |
| 247 | PE-03 | Hardware | transceivers manufacturers | port 14 | PASS |  |
| 248 | PE-03 | Hardware | transceivers manufacturers | port 11 | PASS |  |
| 249 | PE-03 | Hardware | transceivers manufacturers | port 10 | PASS |  |
| 250 | PE-03 | Hardware | transceivers manufacturers | port 39 | PASS |  |
| 251 | PE-03 | Hardware | transceivers manufacturers | port 12 | PASS |  |
| 252 | PE-03 | Hardware | transceivers manufacturers | port 15 | PASS |  |
| 253 | PE-03 | Hardware | transceivers manufacturers | port 48 | PASS |  |
| 254 | PE-03 | Hardware | transceivers manufacturers | port 17 | PASS |  |
| 255 | PE-03 | Hardware | transceivers manufacturers | port 16 | PASS |  |
| 256 | PE-03 | Hardware | transceivers manufacturers | port 19 | PASS |  |
| 257 | PE-03 | Hardware | transceivers manufacturers | port 54 | FAIL | transceivers manufacturers is "Arista Networks " |
| 258 | PE-03 | Hardware | transceivers manufacturers | port 31 | PASS |  |
| 259 | PE-03 | Hardware | transceivers manufacturers | port 49 | PASS |  |
| 260 | PE-03 | Hardware | transceivers manufacturers | port 51 | FAIL | transceivers manufacturers is "Arista Networks " |
| 261 | PE-03 | Hardware | transceivers manufacturers | port 36 | PASS |  |
| 262 | PE-03 | Hardware | transceivers manufacturers | port 53 | FAIL | transceivers manufacturers is "Arista Networks " |
| 263 | PE-03 | Hardware | transceivers manufacturers | port 52 | PASS |  |
| 264 | PE-03 | Hardware | transceivers manufacturers | port 33 | PASS |  |
| 265 | PE-03 | Hardware | transceivers manufacturers | port 55 | FAIL | transceivers manufacturers is "Arista Networks " |
| 266 | PE-03 | Hardware | transceivers manufacturers | port 37 | PASS |  |
| 267 | PE-03 | Hardware | transceivers manufacturers | port 32 | PASS |  |
| 268 | PE-03 | Hardware | transceivers manufacturers | port 50 | FAIL | transceivers manufacturers is "Arista Networks " |
| 269 | PE-04 | Hardware | transceivers manufacturers | port 11 | FAIL | transceivers manufacturers is "Arista Networks " |
| 270 | PE-04 | Hardware | transceivers manufacturers | port 10 | FAIL | transceivers manufacturers is "Arista Networks " |
| 271 | PE-04 | Hardware | transceivers manufacturers | port 6 | PASS |  |
| 272 | PE-04 | Hardware | transceivers manufacturers | port 13 | PASS |  |
| 273 | PE-04 | Hardware | transceivers manufacturers | port 29 | PASS |  |
| 274 | PE-04 | Hardware | transceivers manufacturers | port 12 | PASS |  |
| 275 | PE-04 | Hardware | transceivers manufacturers | port 17 | PASS |  |
| 276 | PE-04 | Hardware | transceivers manufacturers | port 15 | FAIL | transceivers manufacturers is "Arista Networks " |
| 277 | PE-04 | Hardware | transceivers manufacturers | port 23 | PASS |  |
| 278 | PE-04 | Hardware | transceivers manufacturers | port 24 | PASS |  |
| 279 | PE-04 | Hardware | transceivers manufacturers | port 25 | PASS |  |
| 280 | PE-04 | Hardware | transceivers manufacturers | port 26 | PASS |  |
| 281 | PE-04 | Hardware | transceivers manufacturers | port 27 | PASS |  |
| 282 | PE-04 | Hardware | transceivers manufacturers | port 20 | PASS |  |
| 283 | PE-04 | Hardware | transceivers manufacturers | port 21 | PASS |  |
| 284 | PE-04 | Hardware | transceivers manufacturers | port 22 | PASS |  |
| 285 | PE-04 | Hardware | transceivers manufacturers | port 16 | FAIL | transceivers manufacturers is "Arista Networks " |
| 286 | PE-04 | Hardware | transceivers manufacturers | port 19 | PASS |  |
| 287 | PE-04 | Hardware | transceivers manufacturers | port 32 | PASS |  |
| 288 | PE-04 | Hardware | transceivers manufacturers | port 31 | PASS |  |
| 289 | PE-04 | Hardware | transceivers manufacturers | port 30 | PASS |  |
| 290 | PE-04 | Hardware | transceivers manufacturers | port 28 | PASS |  |
| 291 | PE-04 | Hardware | transceivers manufacturers | port 36 | PASS |  |
| 292 | PE-04 | Hardware | transceivers manufacturers | port 35 | PASS |  |
| 293 | PE-04 | Hardware | transceivers manufacturers | port 34 | PASS |  |
| 294 | PE-04 | Hardware | transceivers manufacturers | port 1 | FAIL | transceivers manufacturers is "Arista Networks " |
| 295 | PE-04 | Hardware | transceivers manufacturers | port 33 | PASS |  |
| 296 | PE-04 | Hardware | transceivers manufacturers | port 3 | FAIL | transceivers manufacturers is "Arista Networks " |
| 297 | PE-04 | Hardware | transceivers manufacturers | port 2 | FAIL | transceivers manufacturers is "Arista Networks " |
| 298 | PE-04 | Hardware | transceivers manufacturers | port 5 | FAIL | transceivers manufacturers is "Arista Networks " |
| 299 | PE-04 | Hardware | transceivers manufacturers | port 4 | PASS |  |
| 300 | PE-04 | Hardware | transceivers manufacturers | port 7 | FAIL | transceivers manufacturers is "Arista Networks " |
| 301 | PE-04 | Hardware | transceivers manufacturers | port 18 | PASS |  |
| 302 | PE-04 | Hardware | transceivers manufacturers | port 9 | FAIL | transceivers manufacturers is "Arista Networks " |
| 303 | PE-04 | Hardware | transceivers manufacturers | port 8 | FAIL | transceivers manufacturers is "Arista Networks " |
| 304 | PE-04 | Hardware | transceivers manufacturers | port 14 | PASS |  |
| 305 | P-01 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 306 | P-02 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 307 | PE-01 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 308 | PE-02 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 309 | PE-03 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 310 | PE-04 | NTP | Synchronised with NTP server | NTP | FAIL | not synchronised to NTP server |
| 311 | P-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet1/1 - P2P_LINK_TO_PE-01_Ethernet1/1 | PASS |  |
| 312 | P-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet2/1 - P2P_LINK_TO_PE-02_Ethernet50/1 | PASS |  |
| 313 | P-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet25/1 - P2P_LINK_TO_P-02_Ethernet25/1 | PASS |  |
| 314 | P-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet26/1 - P2P_LINK_TO_PE-03_Ethernet55/1 | PASS |  |
| 315 | P-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet1/1 - P2P_LINK_TO_PE-04_Ethernet1/1 | PASS |  |
| 316 | P-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet2/1 - P2P_LINK_TO_PE-04_Ethernet2/1 | PASS |  |
| 317 | P-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet4/1 - P2P_LINK_TO_PE-03_Ethernet50/1 | PASS |  |
| 318 | P-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet25/1 - P2P_LINK_TO_P-01_Ethernet25/1 | PASS |  |
| 319 | P-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet26/1 - P2P_LINK_TO_PE-02_Ethernet55/1 | PASS |  |
| 320 | PE-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet1/1 - P2P_LINK_TO_P-01_Ethernet1/1 | PASS |  |
| 321 | PE-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet2/1 - P2P_LINK_TO_PE-02_Ethernet49/1 | PASS |  |
| 322 | PE-01 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet5/1 - speed_config_10g | PASS |  |
| 323 | PE-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet49/1 - P2P_LINK_TO_PE-01_Ethernet2/1 | PASS |  |
| 324 | PE-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet50/1 - P2P_LINK_TO_P-01_Ethernet2/1 | PASS |  |
| 325 | PE-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet55/1 - P2P_LINK_TO_P-02_Ethernet26/1 | PASS |  |
| 326 | PE-02 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet52/2 - CPE-1_Ethernet2 | PASS |  |
| 327 | PE-03 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet50/1 - P2P_LINK_TO_P-02_Ethernet4/1 | PASS |  |
| 328 | PE-03 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet55/1 - P2P_LINK_TO_P-01_Ethernet26/1 | PASS |  |
| 329 | PE-04 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet1/1 - P2P_LINK_TO_P-02_Ethernet1/1 | PASS |  |
| 330 | PE-04 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet2/1 - P2P_LINK_TO_P-02_Ethernet2/1 | PASS |  |
| 331 | PE-04 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet5/3 - CPE-2_Ethernet34 | PASS |  |
| 332 | PE-04 | Interface State | Ethernet Interface Status & Line Protocol == "up" | Ethernet5/1 - speed_config_10g | FAIL | interface status: down - line protocol status: down |
| 333 | P-01 | Interface State | Loopback Interface Status & Line Protocol == "up" | Loopback0 - Overlay_Peering | PASS |  |
| 334 | P-02 | Interface State | Loopback Interface Status & Line Protocol == "up" | Loopback0 - Overlay_Peering | PASS |  |
| 335 | PE-01 | Interface State | Loopback Interface Status & Line Protocol == "up" | Loopback0 - Overlay_Peering | PASS |  |
| 336 | PE-02 | Interface State | Loopback Interface Status & Line Protocol == "up" | Loopback0 - Overlay_Peering | PASS |  |
| 337 | PE-03 | Interface State | Loopback Interface Status & Line Protocol == "up" | Loopback0 - Overlay_Peering | PASS |  |
| 338 | PE-04 | Interface State | Loopback Interface Status & Line Protocol == "up" | Loopback0 - Overlay_Peering | PASS |  |
| 339 | P-01 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet1/1 - remote: PE-01_Ethernet1/1 | PASS |  |
| 340 | P-01 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet2/1 - remote: PE-02_Ethernet50/1 | PASS |  |
| 341 | P-01 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet25/1 - remote: P-02_Ethernet25/1 | PASS |  |
| 342 | P-01 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet26/1 - remote: PE-03_Ethernet55/1 | PASS |  |
| 343 | P-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet1/1 - remote: PE-04_Ethernet1/1 | PASS |  |
| 344 | P-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet2/1 - remote: PE-04_Ethernet2/1 | PASS |  |
| 345 | P-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet4/1 - remote: PE-03_Ethernet50/1 | PASS |  |
| 346 | P-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet25/1 - remote: P-01_Ethernet25/1 | PASS |  |
| 347 | P-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet26/1 - remote: PE-02_Ethernet55/1 | PASS |  |
| 348 | PE-01 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet1/1 - remote: P-01_Ethernet1/1 | PASS |  |
| 349 | PE-01 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet2/1 - remote: PE-02_Ethernet49/1 | PASS |  |
| 350 | PE-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet49/1 - remote: PE-01_Ethernet2/1 | PASS |  |
| 351 | PE-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet50/1 - remote: P-01_Ethernet2/1 | PASS |  |
| 352 | PE-02 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet55/1 - remote: P-02_Ethernet26/1 | PASS |  |
| 353 | PE-03 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet50/1 - remote: P-02_Ethernet4/1 | PASS |  |
| 354 | PE-03 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet55/1 - remote: P-01_Ethernet26/1 | PASS |  |
| 355 | PE-04 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet1/1 - remote: P-02_Ethernet1/1 | PASS |  |
| 356 | PE-04 | LLDP Topology | lldp topology - validate peer and interface | local: Ethernet2/1 - remote: P-02_Ethernet2/1 | PASS |  |
| 357 | P-01 | IP Reachability | ip reachability test p2p links | Source: P-01_Ethernet1/1 - Destination: PE-01_Ethernet1/1 | PASS |  |
| 358 | P-01 | IP Reachability | ip reachability test p2p links | Source: P-01_Ethernet2/1 - Destination: PE-02_Ethernet50/1 | PASS |  |
| 359 | P-01 | IP Reachability | ip reachability test p2p links | Source: P-01_Ethernet25/1 - Destination: P-02_Ethernet25/1 | PASS |  |
| 360 | P-01 | IP Reachability | ip reachability test p2p links | Source: P-01_Ethernet26/1 - Destination: PE-03_Ethernet55/1 | PASS |  |
| 361 | P-02 | IP Reachability | ip reachability test p2p links | Source: P-02_Ethernet1/1 - Destination: PE-04_Ethernet1/1 | PASS |  |
| 362 | P-02 | IP Reachability | ip reachability test p2p links | Source: P-02_Ethernet2/1 - Destination: PE-04_Ethernet2/1 | PASS |  |
| 363 | P-02 | IP Reachability | ip reachability test p2p links | Source: P-02_Ethernet4/1 - Destination: PE-03_Ethernet50/1 | PASS |  |
| 364 | P-02 | IP Reachability | ip reachability test p2p links | Source: P-02_Ethernet25/1 - Destination: P-01_Ethernet25/1 | PASS |  |
| 365 | P-02 | IP Reachability | ip reachability test p2p links | Source: P-02_Ethernet26/1 - Destination: PE-02_Ethernet55/1 | PASS |  |
| 366 | PE-01 | IP Reachability | ip reachability test p2p links | Source: PE-01_Ethernet1/1 - Destination: P-01_Ethernet1/1 | PASS |  |
| 367 | PE-01 | IP Reachability | ip reachability test p2p links | Source: PE-01_Ethernet2/1 - Destination: PE-02_Ethernet49/1 | PASS |  |
| 368 | PE-02 | IP Reachability | ip reachability test p2p links | Source: PE-02_Ethernet49/1 - Destination: PE-01_Ethernet2/1 | PASS |  |
| 369 | PE-02 | IP Reachability | ip reachability test p2p links | Source: PE-02_Ethernet50/1 - Destination: P-01_Ethernet2/1 | PASS |  |
| 370 | PE-02 | IP Reachability | ip reachability test p2p links | Source: PE-02_Ethernet55/1 - Destination: P-02_Ethernet26/1 | PASS |  |
| 371 | PE-03 | IP Reachability | ip reachability test p2p links | Source: PE-03_Ethernet50/1 - Destination: P-02_Ethernet4/1 | PASS |  |
| 372 | PE-03 | IP Reachability | ip reachability test p2p links | Source: PE-03_Ethernet55/1 - Destination: P-01_Ethernet26/1 | PASS |  |
| 373 | PE-04 | IP Reachability | ip reachability test p2p links | Source: PE-04_Ethernet1/1 - Destination: P-02_Ethernet1/1 | PASS |  |
| 374 | PE-04 | IP Reachability | ip reachability test p2p links | Source: PE-04_Ethernet2/1 - Destination: P-02_Ethernet2/1 | PASS |  |
| 375 | P-01 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 376 | P-02 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 377 | PE-01 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 378 | PE-02 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 379 | PE-03 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 380 | PE-04 | BGP | ArBGP is configured and operating | ArBGP | PASS |  |
| 381 | P-01 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.1 | PASS |  |
| 382 | P-01 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.2 | PASS |  |
| 383 | P-01 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.3 | PASS |  |
| 384 | P-01 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.4 | PASS |  |
| 385 | P-02 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.1 | PASS |  |
| 386 | P-02 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.2 | PASS |  |
| 387 | P-02 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.3 | PASS |  |
| 388 | P-02 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.4 | PASS |  |
| 389 | PE-01 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.5 | PASS |  |
| 390 | PE-01 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.6 | PASS |  |
| 391 | PE-02 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.5 | PASS |  |
| 392 | PE-02 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.6 | PASS |  |
| 393 | PE-03 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.5 | PASS |  |
| 394 | PE-03 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.6 | PASS |  |
| 395 | PE-04 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.5 | PASS |  |
| 396 | PE-04 | BGP | bgp evpn peer state established (evpn) | bgp_neighbor: 100.70.0.6 | PASS |  |
