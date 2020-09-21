Collections of Business Domain (Financing, Trading and Banking)  in clojure code.  

- interest   
- loan   
- compound interest   
- deprecation  
- investment   
- pension  
- periodic payment   
- share prices   
- root finding  
- ratio   
- annuity  
- credit card validator (lhun algoritm)  


**Interest**   

Interest is a payment from a borrower or deposit-taking from financial institution to a lender as form of compensation at particular rate of sum amount of repayment. the lender or depositor may gain interest from their savings acccording to the rate of interest or  amount paid or recieved over particular period divided by principal sum borrowed.   

references : [https://en.wikipedia.org/wiki/Interest](https://en.wikipedia.org/wiki/Interest)  

```clj

(defn interest-amount
  "Calculates the generated amount of interest for given investment with given rate over a period of time
  "
  [{:keys [present-value rate period]}]  
  {:pre [(number? present-value)
         (number? rate)
         (number? period)]}
  (* present-value rate period))


(interest-amount {:present-value 100
                  :rate 0.05
                  :period 5}) ;; => 25.0;

(interest-amount {:present-value 500
                  :rate 0.1
                  :period 8}) ;; => 400.0;

(interest-amount {:present-value 800 :rate 0.15 :period 12}) ;; => 1440.0


(defn final-interest
  "calculates sum of present value with given interest amounts"
  [{:keys [present-value rate period]}]
  {:pre [(number? present-value)
         (number? rate)
         (number? period)]}
  (+ present-value
    (interest-amount {:present-value present-value
                      :rate rate
                      :period period})))

(final-interest {:present-value 100 :rate 0.05 :period 5}) ;; => 125.0

(final-interest {:present-value 500 :rate 0.1 :period 8}) ;; => 900


(final-interest {:present-value 800 :rate 0.15 :period 12}) ;; => 2240.0


(defn present-value-interest
  "calculates the present value if given final value over rate of period of time"
  [{:keys [final-value rate period]}]
  {:pre [(number? final-value)
         (number? rate)
         (number? period)]}
  (/ final-value
    (inc (* rate period))))

(present-value-interest {:final-value 250 :rate 0.05 :period 5})
;; => 200
(present-value-interest {:final-value 400 :rate 400 :period 8})
;; => 400/3201 or 222.22223
(present-value-interest {:final-value 750 :rate 0.15 :period 12})
;; => 267.8571428571429

(defn rate-interest
  "calcuate required rate of an interest"
  [{:keys [final-value present-value period]}]
  {:pre [(number? final-value)
         (number? present-value)
         (number? period)]}
  (/ (- final-value present-value) (* present-value period)))

(rate-interest {:final-value 300 :present-value 150 :period 5})
;; => 1/5
(rate-interest {:final-value 500 :present-value 180 :period 8})
;; => 2/9
o(rate-interest {:final-value 800 :present-value 230 :period 12})
;; => 19/92

(defn period-interest
  "calculate periods of interest given final-value to reach from present capital at speed of rate interest"
  [{:keys [final-value present-value rate]}]
  {:pre [(number? final-value)
         (number? present-value)
         (number? rate)]}
  (/ (- final-value present-value) (* present-value rate)) )

(period-interest {:final-value 300 :present-value 150 :rate 0.05 })
;; => 20.0

(period-interest {:final-value 500 :present-value 180 :rate 0.1})
;; => 17.7778

(period-interest {:final-value 800 :present-value 230 :rate 0.15})
;; => 16.52173913043478

(defn period-days-interest
  "calculates the number interest days"
  [{:keys [final-value present-value rate]}]
  {:pre [(number? final-value)
         (number? present-value)
         (number? rate)]}
  (* 365
    (/ (- final-value present-value)
      (* present-value rate))))

(period-days-interest {:final-value 300 :present-value 150 :rate 0.05}) ;; => 7300

```


