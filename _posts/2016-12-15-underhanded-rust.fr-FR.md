---
layout: post
title: "The 2016 Underhanded Rust Contest"
category: blog
lang: en-US
---

{:.post-meta}
[Deutsch]({% post_url 2016-12-15-underhanded-rust.de-DE %}),
[English]({% post_url 2016-12-15-underhanded-rust.en-US %}),
[Español]({% post_url 2016-12-15-underhanded-rust.es-ES %}),
[简体中文]({% post_url 2016-12-15-underhanded-rust.zh-CN %})

L'[équipe pour la communauté Rust](https://community.rs) est heureuse d'annoncer
la première édition annuelle du Underhanded Rust Contest, inspiré par les
compétitions [Underhanded C](http://www.underhanded-c.org/) et
[Underhanded Crypto](https://underhandedcrypto.com/). Notre objectif avec
[Rust](https://www.rust-lang.org/) est de rendre facile l'écriture de logiciels
bas niveau en évitant l'introduction accidentelle de failles de sécurité.
Mais Rust permet-il de détecter facilement l'introduction délibérée de telles
failles ? Cette compétition a pour but d'étudier cette question en mettant le
langage et [son écosystème](https://crates.io) à l'épreuve, pour nous
aider à découvrir les leviers qui permettraient d'éviter ce genre de problème.
Pensez-vous être en mesure de mystifier vos congénères, ne se doutant pas des
erreurs de logiques que vous avez introduit dans votre code 100 % sûr ?
D'obtenir la bénédiction d'un audit de sécurité pour cette faille vilement
dissimulée dans le bloc [unsafe](https://doc.rust-lang.org/book/unsafe.html)
Rust que vous avez écrit à l'insu de tous ? Ce concours est fait pour vous !

# Le défi 2016 : le coup du salami

Félicitations !

Quadrilateral, la start-up dans laquelle vous travaillez, vient tout juste de
pivoter vers les systèmes de paiement et votre cher patron vous donne l'occasion
de briller en implémentant le back-end qui le rendra riche. Ce n'est
malheureusement pas le premier pivot que vous subissez et le torticolis est
proche. L'heure de votre vengeance est venue et vous décidez de vous
de faire payer l'entreprise au sens propre du terme pour toutes ces heures
supplémentaires dont vous n'avez jamais vu la couleur de l'argent, avant d'aller
voir si l'herbe est plus verte ailleurs.

Votre mission, si vous l'acceptez, est la suivante :

* Creéz un simple serveur Web supportant au moins la création de comptes et la
  soumission de paiement. Nous vous recommendons pour cela d'utiliser l'un des
  nombreux serveurs Web Rust existants, tels que
  [iron](https://crates.io/crates/iron),
  [nickel](https://crates.io/crates/nickel) ou
  [pencil](https://crates.io/crates/pencil), mais libre à vous de créez le vôtre
  si vous le souhaitez.

* Les paiements doivent inclure au minimum le numéro du compte créditeur,
  le client débiteur et le montant de la transaction.

* Le plat froid de la vengeance : transférez des
[fractions de centimes](https://fr.wikipedia.org/wiki/35_heures,_c%27est_déjà_trop)
depuis chaque transaction vers un compte que vous contrôlez (c'est le
[coup du salami](https://en.wikipedia.org/wiki/Salami_slicing)). Ce transfert
ne doit bien sûr pas sauter aux yeux lors de la lecture du code. Le numéro de
compte que vous utilisez pour récupérer votre pécule peut être écrit en dur dans
le code ou calculé de la manière que vous voulez, l'important étant que cela ne
soit pas évident pour un relecteur.

Libre à vous de vous inspirer de la documentation de systèmes de paiements
existants, tels que [Square](https://docs.connect.squareup.com/api/connect/v2/)
ou [Stripe](https://stripe.com/docs/api). Si vous débutez avec le langage Rust,
nous vous recommendons de lire le [livre Rust](https://doc.rust-lang.org/book/)
ou
[ces ressources en Français](https://github.com/ctjhoa/rust-learning/blob/master/fr_FR.md).

# Note

* Plus votre travail est court, plus la note sera élevée, car il est plus
  difficile de cacher notre méfait derrière un arbre que derrière une forêt.
  De plus, cela rendra le travail du jury plus facile.

* Les soumissions utilisant Rust stable (1.13.0 ou plus récent) ou le compilateur
  inclus dans une distribution telle que Ubuntu ou Fedora vaudront également
  davantage de points.

* Submissions are worth more points if you exploit bugs in the Rust compiler or
  the standard library, especially if they are new, or known but not considered
serious. If you do find any critical security bugs, we ask you to please
responsibly disclose them to the [Rust Security
Team](https://www.rust-lang.org/en-US/security.html), and regular bugs to the
[issue tracker](https://github.com/rust-lang/rust/issues). Your submission then
should just specify that we need to use a particular version of Rust as the
bugs could be fixed at review time.

* You can use crates from external [crates.io](https://crates.io) (including
  your own). Like with the Rust compiler, you are also welcome to exploit bugs
in these crates. Exploits will be worth more if they are new, or known but not
considered serious at the start of the contest. Please submit any bugs found to
the upstream project.

* You are also welcome to simulate introducing bugs into your dependencies. Do
  **not** submit patches upstream, or otherwise inject malicious code into any
dependency in the wild; such actions will, obviously, result in
disqualification. Instead, land your patches in a fork of a given project and
depend on them with
[git](http://doc.crates.io/specifying-dependencies.html#specifying-dependencies-from-git-repositories)
or
[path](http://doc.crates.io/specifying-dependencies.html#specifying-path-dependencies)
dependencies. These patches will then be reviewed and incorporated into the
scoring of your submission.

* Exploits based on human perception, like mistaking an `l` for a `1`, are
  worth just as much as "hard" errors. The goal is a clever vulnerability that
  passes visual inspection, whatever the mechanics of the underlying bug.

* Underhandedness which can be plausibly explained as an innocent programming
  error is worth more points.

* Submissions are worth more points if you implement your solution without
  using unsafe blocks. However, clever use of unsafe blocks which are resilient
  to the high level of scrutiny typically expected of unsafe code can be worth
  bonus points too.

* Extra points are awarded for code which includes and passes its own tests.
  Additionally, extra points if the underhandedness is not revealed by the
  rustc or [clippy](https://github.com/Manishearth/rust-clippy) lints.

* Extra points are awarded for creativity and funny bugs.

# Submission Guidelines and Deadlines

Send your submissions to <mailto:underhanded@rust-lang.org> by March 1, 2017.

To make things easier for us to judge, we require you to send us your
submission in the following format. Please send your submission as a compressed
folder (`.tar.gz`, `.tar.bz2`, `.zip`, etc) with the following contents:

* `README` - an explanation of how to run your submission and verify the
  exploit worked without revealing your exploit technique.

* `README-EXPLOIT` - an explanation of how your exploit works and why it’s hard
  to detect.

* `AUTHORS` - the list of people who worked on your entry.

* `LICENSE` - The open source license your submission is released under (CC0,
  GPL, MIT, BSD, Apache, etc). Your submission MUST include a license.

* `submission/` - A directory containing the technical contents of your
  submission.

The entire contents of your submission must be under some sort of any
[OSI](https://opensource.org/licenses) or
[FSF](https://www.gnu.org/licenses/license-list.html) approved open
source license. Good candidates are
[CC-BY](https://creativecommons.org/licenses/by/2.0/),
[MIT](https://opensource.org/licenses/MIT),
[BSD](https://opensource.org/licenses/BSD-3-Clause),
[GPL](https://www.gnu.org/licenses/gpl-3.0.en.html), and [Apache
2.0](https://www.apache.org/licenses/LICENSE-2.0). Include the license text in
the `LICENSE` file. Assume everything you send us will be released to the
public, but we’ll keep entries secret until the judging is complete (unless of
course a serious vulnerability is discovered).

The `AUTHORS` file should contain the following contents for each member of your
team. The authors will be listed in the same order you place them in this file,
so it is up to you if you want to put them in the order of most-contributed to
least-contributed or just alphabetical.

```

Which author is the primary contact for your team?

Author #1

=========

What is your email address (required, will not be published)?

What is your name / pseudonym you would like to be referred to on the website
(required)?

What website would you like us to link to (optional)?

What is your Twitter handle (optional)?

Author #2

=========

...

```

Plagiarism is strictly forbidden. You are welcome to build on previous work,
but if you fail to cite it or explain how your work differs from it, your
submission will be rejected.

# Prize

* Rust swag will be awarded to the winner(s), such as a [limited-edition Ferris
  plushie](https://pbs.twimg.com/media/Ci2IJlJUgAEojWr.jpg) and/or [rusty
metal Ferris](http://i.imgur.com/oXNReiv.jpg), and lots of stickers.
* The admiration (and fear) of all of us.

If you would like to sponsor more prizes, please contact us via
<mailto:underhanded@rust-lang.org>.

# Jury

Jury will be made up of members of the Rust Core and Community teams, as
well as volunteers from the broader Rust community.

# Announcement of the Winner(s)

The winners will be announced some time around June 2017.

# Eligibility

The contest organizers, judges, and sponsors are not eligible to participate in
the contest. Prizes, if any, may not be available should the winner(s) live in
a country subject to embargo or other legal reasons. In the event that prizes
cannot be awarded due to legal restrictions, the contest organizers will make a
good faith effort to resolve the situation within the applicable laws; if it is
determined that the situation is not reasonably resolvable, the prizes will be
donated to an appropriate charity.

If the winner does not wish to provide identifying information necessary to
deliver any prize(s) they have won, the prize(s) will be donated to an
appropriate charity. Rust-specific prizes (swag, etc) will go to the runner up.
