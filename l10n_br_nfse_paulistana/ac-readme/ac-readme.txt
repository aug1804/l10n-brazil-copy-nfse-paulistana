ac-readme.txt

O repositório 'l10n-brazil-copy-nfse-paulistana' contém apenas o módulo 'l10n_br_nfse_paulistana' já convertido da v15 para a v16 que deve ser copiado (git clone) e instado na sua instância.

Agora ATENÇÃO: o diretório 'ac-readme/l10n_br_nfse' NÃO CONTÉM O MÓDULO 'l10n_br_nfse' COMPLETO, mas apenas os 2 arquivos já devidamente alterados para fazer com que o módulo 'NFSe Paulistana' possa funcionar - se quiser copiá-los para a sua instância, dê antes um 'diff' para se certificar que não há outras alterações a serem feitas, além das abaixo.

Essas são as modificações que devem ser feitas nos 2 arquivos que pertencem ao módulo 'l10n_br_nfse':

1. /l10n-brazil/l10n_br_nfse/models/document.py

(aproximadamente entre as linhas 75 a 88)
#[ac].2026-05-17
#   def make_pdf(self):
#       if not self.filtered(filter_processador_edoc_nfse):
#           return super().make_pdf()
#       pdf = self.env.ref("l10n_br_nfse.report_br_nfse_danfe")._render_qweb_pdf(
#           self.ids
#       )[0]
    def make_pdf(self):
        if not self.filtered(filter_processador_edoc_nfse):
            return super().make_pdf()
        report = self.env.ref("l10n_br_nfse.report_br_nfse_danfe")
        pdf, _ = report.with_context(no_pdfs=False)._render_qweb_pdf("l10n_br_nfse.report_br_nfse_danfe", res_ids=self.ids)
#       return pdf
#[ac].2026-05-17

2. /l10n-brazil/l10n_br_nfse/report/danfse.xml

(aproximadamente entre as linhas 105 a 118)
<!--[ac].2026-05-17 → to_text -->
<!--            <div class="col-2"> -->
<!--                <img -->
<!--                    t-att-src="'data:image/png;base64,%s' % to_text(doc.company_id.nfse_city_logo)" -->
<!--                    style="max-height:80px; margin-top:4px; margin-left:10px;" -->
<!--                /> -->
<!--            </div> -->
                <div class="col-2">
                    <img
                        t-att-src="'data:image/png;base64,%s' % (doc.company_id.nfse_city_logo or '')"
                        style="max-height:80px; margin-top:4px; margin-left:10px;"
                    />
                </div>
<!--[ac].2026-05-17-->

(aproximadamente entre as linhas 195 a 208)
<!--[ac].2026-05-17 → to_text -->
<!--            <div class="col-2"> -->
<!--                <img -->
<!--                    style="max-height: 150px; padding-left: 25px; padding-top: 25px; max-width: 125px;" -->
<!--                    t-att-src="'data:image/png;base64,%s' % to_text(doc.company_id.logo)" -->
<!--                /><br /> -->
<!--            </div> -->
                <div class="col-2">
                    <img
                        style="max-height: 150px; padding-left: 25px; padding-top: 25px; max-width: 125px;"
                        t-att-src="'data:image/png;base64,%s' % (doc.company_id.logo or '')"
                    /><br />
                </div>
<!--[ac].2026-05-17-->

(aproximadamente entre as linhas 464 a 469)
<!--[ac].2026-05-17-->
<!--                <span t-field="doc.amount_untaxed" /> -->
<!--                <span t-field="doc.amount_total" /> -->
<!--                <span t-field="doc.amount_gross" /> tentativa 2 -->
                    <span t-field="doc.amount_price_gross" />
<!--[ac].2026-05-17-->
