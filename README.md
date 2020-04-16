# mySQL-cheatsheet
BT2102 sem 2

## Integrity Control
Defining constraints on col/ table: 
'CHECK (SearchCondition)' eg. SEX CHAR NOT NULL CHECK (sex IN('M', 'F'))

####Creating/ dropping domain:
'''
CREATE DOMAIN domainName [AS] datatype
 [DEFAULT defaultOption]
  [CHECK (SearchCondition)]
  '''
'DROP DOMAIN DomainName [RESTRICT|CASCADE]'
RESTRICT: if domain is used in existing table, drop fails
CASCADE: table columns dependent on domain will use underlying data type, domain consntraints replaced by column constraints

####Primary Key
define pri key: 'PRIMARY KEY (attributeName)'
composite primary key: 'PRIMARY KEY (key1, key2)'

##aggregate functions

selecting **max** : 
'''
SELECT c1, c2 
  FROM tableName 
    WHERE c1 = (SELECT MAX (c1) 
                  FROM tableName);
                  '''
                  
selecting distinct and not null: 
'''
SELECT DISTINCT c1, c2 
  FROM tableName 
    WHERE c1 IS NOT NULL 
      ORDER BY c1, c2;
      '''

