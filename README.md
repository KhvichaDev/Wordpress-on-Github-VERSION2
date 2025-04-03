# Wordpress + phpMyAdmin on Github Codespace

ეს პროექტი უზრუნველყოფს მზა სამუშაო გარემოს WordPress-ის და phpMyAdmin-ისთვის GitHub Codespaces-ში. ის ავტომატურად აკონფიგურირებს საჭირო სერვისებს და გარემოს WordPress პროექტების სწრაფად დასაწყებად.

## აღწერა

ეს devcontainer-ის კონფიგურაცია იყენებს Docker-ს, რათა შექმნას კონტეინერი, რომელშიც გაშვებულია:

* Apache: ვებ სერვერი WordPress-თვის.
* MySQL: მონაცემთა ბაზის სერვერი WordPress-ის და phpMyAdmin-თვის.
* phpMyAdmin: ვებზე დაფუძნებული ინტერფეისი MySQL-ის სამართავად.
* WP-CLI: ბრძანების ხაზის ინსტრუმენტი WordPress-ის სამართავად.

კონფიგურაცია ავტომატურად ასრულებს შემდეგ ნაბიჯებს კონტეინერის გაშვებისას:

1.  იწყებს MySQL და Apache სერვისებს.
2.  აკონფიგურირებს MySQL-ის root მომხმარებელს და ქმნის საჭირო მონაცემთა ბაზებს (`wp_db`, `phpmyadmin`) და მომხმარებლებს (`wp_user`, `pma`).
3.  აინსტალირებს phpMyAdmin-ის სქემას.
4.  ამოწმებს, არსებობს თუ არა WordPress-ის კონფიგურაციის ფაილი (`wp-config.php`). თუ არ არსებობს:
    * ჩამოტვირთავს WordPress-ის უახლეს ვერსიას.
    * ქმნის WordPress-ის კონფიგურაციის ფაილს მონაცემთა ბაზის დეტალებით.
    * აყენებს WordPress-ს საწყისი პარამეტრებით (სათაური, ადმინისტრატორის მომხმარებელი/პაროლი, ელფოსტა).
    * აყენებს შესაბამის ნებართვებს WordPress-ის ფაილებისთვის.
5.  ააქტიურებს Apache-ის `rewrite`, `headers` და `ssl` მოდულებს.
6.  აკონფიგურირებს Apache-ს ვირტუალურ ჰოსტს WordPress-ისთვის 80 პორტზე და phpMyAdmin-ისთვის 8080 პორტზე.

## გამოყენება

* Codespace-ის შექმნის შემდეგ, გარემო ავტომატურად აეწყობა.
* WordPress ხელმისაწვდომი იქნება Codespace-ის URL-ზე 80 პორტზე.
* phpMyAdmin ხელმისაწვდომი იქნება Codespace-ის URL-ზე 8080 პორტზე.
* Wordpress Admin:
                  Username: admin
                  Password: admin123
* phpMyAdmin:
             Username: root
             Password: rootpass

## კონფიგურაცია

* `.devcontainer/devcontainer.json`: შეიცავს Codespace-ის კონფიგურაციის პარამეტრებს, როგორიცაა Docker-ის build-ის პარამეტრები, სამუშაო დირექტორია, პორტების გადამისამართება და post-create ბრძანებები.
* `.devcontainer/Dockerfile`: გამოიყენება Docker-ის image-ის შესაქმნელად, რომელიც შეიცავს საჭირო პროგრამულ უზრუნველყოფას (Ubuntu, Apache, MySQL, PHP, phpMyAdmin, WP-CLI).

## დამატებითი ინფორმაცია

* **WordPress:** [https://wordpress.org/](https://wordpress.org/)
* **phpMyAdmin:** [https://www.phpmyadmin.net/](https://www.phpmyadmin.net/)
* **WP-CLI:** [https://wp-cli.org/](https://wp-cli.org/)
* **GitHub Codespaces:** [https://github.com/features/codespaces](https://github.com/features/codespaces)

---
