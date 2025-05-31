import { z } from 'zod';

export const GtagConfigParamsSchema = z.object({
  'allow_ad_personalization_signals': z.boolean().optional(),
  'allow_google_signals': z.boolean().optional(),
  'cookie_domain': z.string().optional(),
  'cookie_expires': z.number().optional(),
  'cookie_flags': z.string().optional(),
  'cookie_prefix': z.string().optional(),
  'cookie_update': z.boolean().optional(),
  'page_location': z.string().optional(),
  'page_title': z.string().optional(),
  'send_page_view': z.boolean().optional(),
}).strict();

export type GtagConfigParams = z.infer<typeof GtagConfigParamsSchema>;

export interface GtagConfigParams {
  'allow_ad_personalization_signals'?: boolean;
  'allow_google_signals'?: boolean;
  'cookie_domain'?: string;
  'cookie_expires'?: number;
  'cookie_flags'?: string;
  'cookie_prefix'?: string;
  'cookie_update'?: boolean;
  'page_location'?: string;
  'page_title'?: string;
  'send_page_view'?: boolean;
}

