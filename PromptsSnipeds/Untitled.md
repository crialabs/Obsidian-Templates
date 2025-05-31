Um conjunto de configurações comuns do Google Analytics reconhecidas por `gtag.js`.

**Assinatura:**

```
export interface GtagConfigParams 
```

## Propriedades

|Propriedade|Tipo|Descrição|
|---|---|---|
|[allow_ad_personalization_signals](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamsallow_ad_personalization_signals) (link em inglês)|booleano|Se a política for definida como falsa, toda a personalização de publicidade com `gtag.js` será desativada. Consulte [Desativar os Recursos de publicidade](https://developers.google.com/analytics/devguides/collection/ga4/display-features?hl=pt-br).|
|[allow_google_signals](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamsallow_google_signals) (link em inglês)|booleano|Se a política for definida como falsa, todos os Recursos de publicidade com `gtag.js` serão desativados. Consulte [Desativar os Recursos de publicidade](https://developers.google.com/analytics/devguides/collection/ga4/display-features?hl=pt-br).|
|[cookie_domain](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamscookie_domain)|string|O valor padrão é `auto`. Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)|
|[cookie_expires](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamscookie_expires) (em inglês)|number|O padrão é 6.307 2.000 (dois anos, em segundos). Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)|
|[cookie_flags](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamscookie_flags) (em inglês)|string|Quando definidas, anexam mais sinalizações ao cookie. Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)|
|[prefixo_de_cookie](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamscookie_prefix)|string|O valor padrão é `_ga`. Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)|
|[cookie_update](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamscookie_update) [link em inglês]|booleano|Se definida como verdadeira, atualizará os cookies em cada carregamento de página. O padrão é "true". Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)|
|[page_location](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamspage_location)|string|URL da página. Consulte [Visualizações de página](https://developers.google.com/analytics/devguides/collection/ga4/views?hl=pt-br).|
|[page_title](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamspage_title)|string|Título da página. Consulte [Visualizações de página](https://developers.google.com/analytics/devguides/collection/ga4/views?hl=pt-br).|
|[send_page_view](https://firebase.google.com/docs/reference/js/analytics.gtagconfigparams.md?hl=pt-br#gtagconfigparamssend_page_view) (em inglês)|booleano|Se uma visualização de página deve ou não ser enviada. Se for definida como verdadeira (padrão), uma visualização de página será enviada automaticamente após a inicialização da análise. Consulte [Visualizações de página](https://developers.google.com/analytics/devguides/collection/ga4/views?hl=pt-br).|

## GtagConfigParams.allow_ad_personalization_signals

Se a política for definida como falsa, toda a personalização de publicidade com `gtag.js` será desativada. Consulte [Desativar os Recursos de publicidade](https://developers.google.com/analytics/devguides/collection/ga4/display-features?hl=pt-br).

**Assinatura:**

```
'allow_ad_personalization_signals'?: boolean;
```

## GtagConfigParams.allow_google_signals

Se a política for definida como falsa, todos os Recursos de publicidade com `gtag.js` serão desativados. Consulte [Desativar os Recursos de publicidade](https://developers.google.com/analytics/devguides/collection/ga4/display-features?hl=pt-br).

**Assinatura:**

```
'allow_google_signals'?: boolean;
```

## GtagConfigParams.cookie_domain

O padrão é `auto`. Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)

**Assinatura:**

```
'cookie_domain'?: string;
```

## GtagConfigParams.cookie_expires

O padrão é 6.307 2.000 (dois anos, em segundos). Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)

**Assinatura:**

```
'cookie_expires'?: number;
```

## GtagConfigParams.cookie_flags

Quando definidas, anexam mais sinalizações ao cookie. Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)

**Assinatura:**

```
'cookie_flags'?: string;
```

## GtagConfigParams.cookie_prefix

O padrão é `_ga`. Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)

**Assinatura:**

```
'cookie_prefix'?: string;
```

## GtagConfigParams.cookie_update

Se definida como verdadeira, atualizará os cookies em cada carregamento de página. O padrão é "true". Consulte [Cookies e identificação do usuário](https://developers.google.com/analytics/devguides/collection/ga4/cookies-user-id?hl=pt-br)

**Assinatura:**

```
'cookie_update'?: boolean;
```

## GtagConfigParams.page_location

URL da página. Consulte [Visualizações de página](https://developers.google.com/analytics/devguides/collection/ga4/views?hl=pt-br).

**Assinatura:**

```
'page_location'?: string;
```

## GtagConfigParams.page_title

Título da página. Consulte [Visualizações de página](https://developers.google.com/analytics/devguides/collection/ga4/views?hl=pt-br).

**Assinatura:**

```
'page_title'?: string;
```

## GtagConfigParams.send_page_view

Se uma visualização de página deve ou não ser enviada. Se for definida como verdadeira (padrão), uma visualização de página será enviada automaticamente após a inicialização da análise. Consulte [Visualizações de página](https://developers.google.com/analytics/devguides/collection/ga4/views?hl=pt-br).

**Assinatura:**

```
'send_page_view'?: boolean;
```