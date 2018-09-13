# query-foot

(defun testfunction ()
  "nur ein test"
  (interactive)
  (while (search-forward-regexp "\\\\footnote[ 
]*{" nil t)
    (backward-char 1)
    (sp-forward-sexp)
    (backward-char 1)
    (when (looking-back "[^.]")
      (let ((antwort (read-char-choice "Punkt hier einfügen? [y] ja; [n] nein; [i] punkt vor index{} [r] recursive-edit: " '(?y ?i ?n ?r))))
	(cond ((eq antwort ?y) (insert "."))
	      ((eq antwort ?i) (search-backward "\\index")
	       (insert "."))
	      ((eq antwort ?n))
	      ((eq antwort ?r) (message "du bist nun im rekursiven edit. [C-M-c] um diesen zu beenden und fortzufahren")
	       (recursive-edit))
	      )
	)
      )
    )
  (message "bin durch")
  )
