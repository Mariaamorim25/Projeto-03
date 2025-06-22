## 2.1 Processar e preparar a base de dados

### 2.1.1 Conectar/importar dados para ferramentas



### 2.1.2 Identificar e tratar valores nulos

- Identificação dos valores nulos

I. Tabela default - Não foram localizados valores nulos
```sql
SELECT
COUNT(*) AS total_linhas,
COUNTIF(user_id IS NULL) AS user_id_nulos,
COUNTIF(default_flag IS NULL) AS default_flag_nulos,
FROM `projeto-03-super-caja.projeto_03_risco_relativo.default`;
```

II. Tabela loans_detail - Não foram localizados valores nulos
```sql
SELECT
COUNT(*) AS total_linhas,
COUNTIF(user_id IS NULL) AS user_id_nulos,
COUNTIF(more_90_days_overdue IS NULL) AS more_90_days_overdue_nulos,
COUNTIF(using_lines_not_secured_personal_assets IS NULL) AS using_lines_not_secured_personal_assets_nulos,
COUNTIF(number_times_delayed_payment_loan_30_59_days IS NULL) AS number_times_delayed_payment_loan_30_59_days_nulos,
COUNTIF(debt_ratio IS NULL) AS debt_ratio_nulos,
COUNTIF(number_times_delayed_payment_loan_60_89_days IS NULL) AS number_times_delayed_payment_loan_60_89_days_nulos,
FROM `projeto-03-super-caja.projeto_03_risco_relativo.loans_detail`;
```

III. Tabela loans_outstanding - Não foram localizados valores nulos
```sql
SELECT
COUNT(*) AS total_linhas,
COUNTIF(user_id IS NULL) AS user_id_nulos,
COUNTIF(loan_id IS NULL) AS loan_id_nulos,
COUNTIF(loan_type IS NULL) AS loan_types_nulos,
FROM `projeto-03-super-caja.projeto_03_risco_relativo.loans_outstanding`;
```

IV. Tabela user_info - Foram localizados 7.199 valores nulos na coluna last_month_salary e 943 na coluna number_dependents
```sql
SELECT
COUNT(*) AS total_linhas,
COUNTIF(user_id IS NULL) AS user_id_nulos,
COUNTIF(age IS NULL) AS age_nulos,
COUNTIF(sex IS NULL) AS sex_nulos,
COUNTIF(last_month_salary IS NULL) AS last_month_salary_nulos,
COUNTIF(number_dependents IS NULL) AS number_dependents_nulos,
FROM `projeto-03-super-caja.projeto_03_risco_relativo.user_info`;
```

- Tratamento dos valores nulos

I. Juntar a tabela user_info e default 
```sql
CREATE OR REPLACE VIEW `projeto-03-super-caja.projeto_03_risco_relativo.user_info_default` AS
SELECT 
t1.user_id,
t1.age,
t1.sex,
t1.last_month_salary,
t1.number_dependents,
t2.default_flag,
FROM `projeto-03-super-caja.projeto_03_risco_relativo.user_info` AS t1
LEFT JOIN `projeto-03-super-caja.projeto_03_risco_relativo.default` AS t2 
ON t1.user_id = t2.user_id;
```

II. 
